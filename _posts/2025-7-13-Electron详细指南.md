## 使用 Electron 构建表情包管理器：详细指南



核心思想非常强大：利用你现有的 **Web 前端 (HTML/CSS/JS)** 技术来构建一个可以在 **Windows、macOS 和 Linux** 上运行的桌面应用程序。这意味着你可以用前端开发经验来构建美观的用户界面，同时拥有 **Node.js** 的能力来访问本地文件系统和轻量级的 **SQLite 数据库**。

------



### 1. 技术栈选择与环境搭建



你选择的技术栈很棒。以下是回顾和一些额外的说明：

- **前端框架 (推荐):** React, Vue, Angular, Svelte。这些框架能帮助你更好地组织和管理 UI 组件，提高开发效率。在本指南中，我们将采用与框架无关的 UI 概念，但使用其中一个将大大提高复杂 UI 的可维护性。
- **后端/桌面层:** Electron (内置 Chromium 和 Node.js)。
- **数据库:** SQLite (通过 `sqlite3` 或性能更好的 `better-sqlite3` npm 包)。
- **其他工具:** `npm` (或 `yarn`，包管理器), `electron-forge` (Electron 官方推荐的开发工具)。



#### 环境搭建步骤：



1. **安装 Node.js：** 访问 [nodejs.org](https://nodejs.org/) 下载并安装 **LTS (长期支持)** 版本。`npm` 会随 Node.js 一起安装。

2. **全局安装 Electron Forge：**

   Bash

   ```
   npm install -g electron-forge
   ```

   这个命令让 `electron-forge` 作为一个命令行工具可用。

3. **创建新项目：**

   Bash

   ```
   electron-forge init my-emoji-manager --template=webpack-typescript # 或者 --template=webpack
   cd my-emoji-manager
   ```

   这个命令会创建一个基本的 Electron 项目骨架，设置 `webpack` 用于打包，并包含 TypeScript 支持（如果你选择的话）。如果你不习惯 TypeScript，只需省略 `--template=webpack-typescript`，使用 `--template=webpack` 来设置一个基于 JavaScript 的项目。

4. **启动开发模式：**

   Bash

   ```
   npm start
   ```

   这个命令会以开发模式启动你的 Electron 应用程序，并支持热重载。

------



### 2. 项目结构详解



`electron-forge` 模板提供了一个组织良好的起点。让我们看看关键的文件和文件夹：

```
my-emoji-manager/
├── package.json           # 项目配置，依赖，脚本
├── forge.config.js        # Electron Forge 配置，用于打包和发布
├── src/
│   ├── main.ts            # Electron **主进程**代码 (Node.js 环境)
│   ├── preload.ts         # **预加载脚本** (安全桥接主进程和渲染进程)
│   ├── renderer.ts        # **渲染进程**入口 (你的前端代码)
│   ├── index.html         # 渲染进程的 HTML 模板
│   ├── assets/            # (你自己创建) 用于存放管理的表情包文件
│   └── database/          # (你自己创建) 用于存放 SQLite 数据库文件 (比如 emoji.db)
├── .gitignore             # Git 忽略文件
└── README.md              # 项目 README
```



#### 关键角色：



- **`main.ts` (主进程):**
  - 这是你的 Electron 应用的 **Node.js 环境**部分。
  - **负责创建和管理浏览器窗口。**
  - 处理**系统级操作**，如文件系统访问（读、写、删除、复制文件）。
  - 直接与 **SQLite 数据库**交互（查询、插入、更新、删除数据）。
  - 通过 **IPC (进程间通信)** 监听并响应来自渲染进程的请求。
  - 使用 Node.js 内置模块 (`fs`, `path`) 和外部 npm 包 (`sqlite3`)。
- **`preload.ts` (预加载脚本):**
  - **至关重要，这个脚本在渲染进程加载之前运行，但与主进程处于相同的 Node.js 上下文。**
  - 它充当主进程和渲染进程之间的**安全桥梁**。
  - **绝不能直接将 Node.js API 暴露给渲染进程！** 相反，使用 `contextBridge.exposeInMainWorld` 为渲染进程创建一个受控、安全的 API。这可以防止渲染进程中的恶意脚本访问你的系统。
- **`renderer.ts` (渲染进程):**
  - 这里是你的**前端 UI 代码**（例如 React、Vue 或原生 JavaScript）。
  - 它是一个 **Chromium 浏览器环境**，类似于一个网页。
  - **只通过 `preload.ts` 暴露的 API 与主进程通信**，发送请求（例如“扫描表情包”、“删除表情包”）。
  - 负责渲染表情包列表、搜索框、筛选器等 UI 元素。
- **`assets/`:** 这个目录将存放你的应用程序管理的实际表情包图像和 GIF 文件。这些文件通常在用户“导入”它们时从其原始位置复制到这里。
- **`database/`:** 这个文件夹将包含你的 SQLite 数据库文件（例如 `emojis.db`）。

------



### 3. 核心功能模块实现细节



让我们更深入地探讨表情包管理器核心功能的实际实现。

------



#### 3.1 数据存储 (SQLite)



**数据库文件位置：** 最佳实践是将用户特定的数据（如 SQLite 数据库）存储在用户的**应用程序数据目录**中。Electron 提供了 `app.getPath('userData')` 来实现此目的。

TypeScript

```
// main.ts
import { app } from 'electron';
import * as path from 'path';
import * as fs from 'fs'; // 导入 fs 用于创建目录
import sqlite3 from 'sqlite3'; // 或者 'better-sqlite3' 性能更好

// 定义数据库路径
const dbDirectory = path.join(app.getPath('userData'), 'database');
const dbPath = path.join(dbDirectory, 'emojis.db');

let db: sqlite3.Database;

/**
 * 初始化 SQLite 数据库，如果表情包表不存在则创建。
 */
function initDatabase(): Promise<void> {
    return new Promise((resolve, reject) => {
        // 确保数据库目录存在
        if (!fs.existsSync(dbDirectory)) {
            fs.mkdirSync(dbDirectory, { recursive: true });
        }

        db = new sqlite3.Database(dbPath, sqlite3.OPEN_READWRITE | sqlite3.OPEN_CREATE, (err) => {
            if (err) {
                console.error('无法连接到数据库', err);
                return reject(err);
            }
            console.log('已连接到 SQLite 数据库。');

            // 创建 emojis 表
            db.run(`
                CREATE TABLE IF NOT EXISTS emojis (
                    id INTEGER PRIMARY KEY AUTOINCREMENT,
                    name TEXT NOT NULL,         -- 例如 "happy_cat.gif"
                    path TEXT NOT NULL UNIQUE,  -- 在表情包存储目录中的相对路径
                    size INTEGER,               -- 文件大小 (字节)
                    type TEXT,                  -- 文件类型 (gif, png, jpg, webp)
                    tags TEXT,                  -- 标签，可以存储为逗号分隔的字符串或 JSON 数组
                    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
                    last_used_at DATETIME
                );
            `, (createErr) => {
                if (createErr) {
                    console.error('创建表错误', createErr);
                    return reject(createErr);
                }
                console.log('Emojis 表已确保存在。');
                resolve();
            });
        });
    });
}

// 确保应用程序准备就绪时初始化数据库
app.whenReady().then(initDatabase).catch(err => {
    console.error('初始化数据库失败:', err);
    app.quit(); // 如果数据库无法初始化则退出
});

// --- 数据库 CRUD 操作 (主进程) ---

/**
 * 在数据库中插入新的表情包记录。
 * @param emojiData - 包含表情包详细信息的对象。
 * @returns Promise，解析后返回最后插入的 ID。
 */
export function insertEmoji(emojiData: { name: string, path: string, size: number, type: string, tags?: string }): Promise<number> {
    return new Promise((resolve, reject) => {
        db.run(`INSERT INTO emojis (name, path, size, type, tags) VALUES (?, ?, ?, ?, ?)`,
            [emojiData.name, emojiData.path, emojiData.size, emojiData.type, emojiData.tags || ''],
            function(err) {
                if (err) {
                    reject(err);
                } else {
                    resolve(this.lastID); // 'this.lastID' 返回新行的 ID
                }
            }
        );
    });
}

/**
 * 从数据库中检索所有表情包记录。
 * @returns Promise，解析后返回表情包记录数组。
 */
export function getAllEmojis(): Promise<any[]> {
    return new Promise((resolve, reject) => {
        db.all(`SELECT * FROM emojis ORDER BY created_at DESC`, [], (err, rows) => {
            if (err) {
                reject(err);
            } else {
                resolve(rows);
            }
        });
    });
}

/**
 * 根据 ID 删除表情包记录。
 * @param ids - 要删除的表情包 ID 数组。
 * @returns Promise，在删除完成时解析。
 */
export function deleteEmojisByIds(ids: number[]): Promise<void> {
    return new Promise((resolve, reject) => {
        if (ids.length === 0) return resolve();
        const placeholders = ids.map(() => '?').join(',');
        db.run(`DELETE FROM emojis WHERE id IN (${placeholders})`, ids, function(err) {
            if (err) {
                reject(err);
            } else {
                resolve();
            }
        });
    });
}

/**
 * 更新特定表情包的标签。
 * @param id - 要更新的表情包 ID。
 * @param tags - 新的标签字符串。
 * @returns Promise，在更新完成时解析。
 */
export function updateEmojiTags(id: number, tags: string): Promise<void> {
    return new Promise((resolve, reject) => {
        db.run(`UPDATE emojis SET tags = ? WHERE id = ?`, [tags, id], function(err) {
            if (err) {
                reject(err);
            } else {
                resolve();
            }
        });
    });
}

/**
 * 按名称或标签搜索表情包。
 * @param query - 搜索字符串。
 * @returns Promise，解析后返回匹配的表情包记录。
 */
export function searchEmojis(query: string): Promise<any[]> {
    return new Promise((resolve, reject) => {
        const searchTerm = `%${query}%`;
        db.all(`SELECT * FROM emojis WHERE name LIKE ? OR tags LIKE ? ORDER BY created_at DESC`, [searchTerm, searchTerm], (err, rows) => {
            if (err) {
                reject(err);
            } else {
                resolve(rows);
            }
        });
    });
}
```

------



#### 3.2 表情包文件管理



这是 Node.js 的 `fs` (文件系统) 模块在**主进程**中发挥作用的地方。

**定义表情包存储路径：**

TypeScript

```
// main.ts (添加到顶部，与其他路径定义一起)
const emojiStoragePath = path.join(app.getPath('userData'), 'emojis');

// 确保应用准备就绪时目录存在
app.whenReady().then(() => {
    if (!fs.existsSync(emojiStoragePath)) {
        fs.mkdirSync(emojiStoragePath, { recursive: true });
        console.log(`已创建表情包存储目录: ${emojiStoragePath}`);
    }
}).catch(err => {
    console.error('未能确保表情包存储目录:', err);
});
```

**扫描/导入表情包：**

这涉及渲染进程和主进程之间的通信。

1. **用户操作 (渲染进程):** 用户点击“导入”按钮，或将文件拖放到应用程序界面。

2. **选择文件/文件夹 (通过 IPC 的主进程):**

   - **`preload.ts`:** 暴露一个函数来触发文件对话框。

     TypeScript

     ```
     // preload.ts
     import { contextBridge, ipcRenderer } from 'electron';
     
     contextBridge.exposeInMainWorld('electronAPI', {
         openFileDialog: () => ipcRenderer.invoke('dialog:openFile'),
         // ... 其他 API
     });
     ```

   - **`main.ts`:** 监听 IPC 请求并显示对话框。

     TypeScript

     ```
     // main.ts
     import { dialog, ipcMain } from 'electron';
     // ... 其他导入和函数
     
     ipcMain.handle('dialog:openFile', async (event) => {
         const { canceled, filePaths } = await dialog.showOpenDialog({
             properties: ['openFile', 'multiSelections'], // 允许选择多个文件
             filters: [
                 { name: 'Images', extensions: ['gif', 'png', 'jpg', 'jpeg', 'webp'] }
             ]
         });
         if (canceled) {
             return [];
         } else {
             return filePaths;
         }
     });
     ```

3. **处理文件 (主进程):**

   - 在 `dialog:openFile` 向主进程返回 `filePaths` 后，遍历这些路径。

   - 对于每个文件：

     - 读取文件元数据：`fs.statSync(filePath)` 获取 `size`。

     - 为复制的文件生成一个**唯一的文件名**以避免冲突。常见策略是使用 `UUID` 或 `原始文件名_时间戳.ext`。

       TypeScript

       ```
       // main.ts 中生成唯一文件名的示例
       import { v4 as uuidv4 } from 'uuid'; // npm install uuid; npm install @types/uuid
       // ...
       function generateUniqueFilename(originalName: string): string {
           const ext = path.extname(originalName);
           const baseName = path.basename(originalName, ext);
           return `${baseName}_${uuidv4()}${ext}`; // 或者直接 uuidv4() + ext 以确保真正唯一
       }
       ```

     - **复制文件：** `fs.copyFileSync(originalPath, newFullPathInStorage)`。

     - **将元数据插入 SQLite：** 使用你之前定义的 `insertEmoji` 函数。数据库中存储的 `path` 应该是相对于 `emojiStoragePath` 的**相对路径**。

   TypeScript

   ```
   // main.ts
   // ...
   import { insertEmoji, getAllEmojis } from './database'; // 假设数据库函数在 database.ts 或类似文件中
   
   ipcMain.handle('emoji:importFiles', async (event, filePaths: string[]) => {
       const importedEmojis: any[] = [];
       for (const originalPath of filePaths) {
           try {
               const stats = fs.statSync(originalPath);
               if (stats.isFile()) {
                   const originalName = path.basename(originalPath);
                   const newFileName = generateUniqueFilename(originalName); // 实现 generateUniqueFilename
                   const destinationPath = path.join(emojiStoragePath, newFileName);
   
                   fs.copyFileSync(originalPath, destinationPath);
   
                   const emojiData = {
                       name: originalName, // 存储原始名称用于显示
                       path: newFileName,   // 存储相对路径
                       size: stats.size,
                       type: path.extname(originalName).slice(1), // 移除点
                       tags: '' // 初始化为空标签
                   };
                   const id = await insertEmoji(emojiData);
                   importedEmojis.push({ id, ...emojiData });
               }
           } catch (error) {
               console.error(`导入文件 ${originalPath} 失败:`, error);
               // 处理错误，也许向渲染器发送通知
           }
       }
       // 导入后，通知渲染器刷新表情包列表
       event.sender.send('update-emoji-list'); // 参见 preload.ts 中的 'onEmojiUpdate'
       return importedEmojis; // 返回新导入的表情包
   });
   ```

**预览：** 在渲染进程中，一旦你有了表情包数据（包括 `path` 字段，它是 `emojiStoragePath` 中的相对文件名），你就可以显示它们：

HTML

```
<img src="file://${fullEmojiStoragePath}/${emoji.path}" alt="${emoji.name}" />
```

**重要：** 你需要安全地将 `fullEmojiStoragePath` 从主进程传递到渲染进程，或者如果需要，在渲染器中使用一个等效的 `app.getPath('userData')` 来构建它，尽管为显示目的传递绝对路径通常更简单。

**`preload.ts` 用于暴露完整路径：**

TypeScript

```
// preload.ts
import { contextBridge, ipcRenderer } from 'electron';
import * as path from 'path'; // 在这里不能使用 app.getPath，但可以根据 IPC 构建
// 或者更好的是，主进程在应用启动时发送完整路径

contextBridge.exposeInMainWorld('electronAPI', {
    openFileDialog: () => ipcRenderer.invoke('dialog:openFile'),
    getEmojis: () => ipcRenderer.invoke('db:getEmojis'),
    addEmoji: (data: any) => ipcRenderer.invoke('db:addEmoji', data),
    deleteEmojis: (ids: number[]) => ipcRenderer.invoke('db:deleteEmojis', ids),
    updateEmojiTags: (id: number, tags: string) => ipcRenderer.invoke('db:updateEmojiTags', id, tags),
    exportEmojis: (ids: number[]) => ipcRenderer.invoke('export-emojis', ids),
    searchEmojis: (query: string) => ipcRenderer.invoke('db:searchEmojis', query),
    getEmojiStoragePath: () => ipcRenderer.invoke('app:getEmojiStoragePath'), // 暴露路径
    onEmojiUpdate: (callback: (event: any, emojiData: any) => void) => ipcRenderer.on('update-emoji-list', callback)
});
```

**`main.ts` 提供表情包存储路径：**

TypeScript

```
// main.ts
ipcMain.handle('app:getEmojiStoragePath', () => {
    return emojiStoragePath; // 这是完整的绝对路径
});
```

然后在你的渲染器中，你可以获取 `window.electronAPI.getEmojiStoragePath()` 一次并使用它。

**添加/删除/修改：**

- **删除：**

  - **渲染器：** 用户选择表情包，点击删除。将 `emojiIds` 发送到主进程。

  - **主进程：**

    TypeScript

    ```
    // main.ts
    // ... (假设你已经有了 3.1 中的 deleteEmojisByIds 函数)
    ipcMain.handle('db:deleteEmojis', async (event, ids: number[]) => {
        try {
            // 获取要删除文件的表情包路径
            const emojisToDelete = await new Promise<any[]>((resolve, reject) => {
                if (ids.length === 0) return resolve([]);
                const placeholders = ids.map(() => '?').join(',');
                db.all(`SELECT path FROM emojis WHERE id IN (${placeholders})`, ids, (err, rows) => {
                    if (err) reject(err);
                    else resolve(rows);
                });
            });
    
            // 删除文件
            for (const emoji of emojisToDelete) {
                const fullPath = path.join(emojiStoragePath, emoji.path);
                if (fs.existsSync(fullPath)) {
                    fs.unlinkSync(fullPath);
                    console.log(`已删除文件: ${fullPath}`);
                }
            }
    
            // 删除数据库记录
            await deleteEmojisByIds(ids); // 你的 3.1 中的函数
            event.sender.send('update-emoji-list'); // 通知渲染器
            return { success: true };
        } catch (error) {
            console.error('删除表情包错误:', error);
            return { success: false, error: error.message };
        }
    });
    ```

- **添加/修改标签：**

  - **渲染器：** 用于编辑标签的 UI。将 `emojiId` 和 `newTags` 字符串发送到主进程。

  - **主进程：**

    TypeScript

    ```
    // main.ts
    // ... (假设你已经有了 3.1 中的 updateEmojiTags 函数)
    ipcMain.handle('db:updateEmojiTags', async (event, id: number, tags: string) => {
        try {
            await updateEmojiTags(id, tags); // 你的 3.1 中的函数
            event.sender.send('update-emoji-list'); // 通知渲染器
            return { success: true };
        } catch (error) {
            console.error('更新标签错误:', error);
            return { success: false, error: error.message };
        }
    });
    ```

- **搜索/筛选：**

  - **渲染器：** 搜索查询的输入字段。将 `query` 字符串发送到主进程。

  - **主进程：**

    TypeScript

    ```
    // main.ts
    // ... (假设你已经有了 3.1 中的 searchEmojis 函数)
    ipcMain.handle('db:searchEmojis', async (event, query: string) => {
        try {
            const results = await searchEmojis(query); // 你的 3.1 中的函数
            return results;
        } catch (error) {
            console.error('搜索表情包错误:', error);
            return [];
        }
    });
    ```

- **批量处理：**

  - 前端 UI 应该支持多选功能（例如复选框）。
  - 当点击“批量删除”或“批量添加标签”等按钮时，收集所有选定的表情包 ID。
  - 通过单个 IPC 调用（例如 `window.electronAPI.deleteEmojis(selectedIds)`）将 ID 数组发送到主进程。主进程然后遍历 ID 以执行文件删除和数据库更新。

------



#### 3.3 导出功能



将选定的表情包导出为 ZIP 文件是一个很棒的功能。

1. **用户操作 (渲染器):** 用户选择表情包，点击“导出”。将选定的 `emojiIds` 发送到主进程。

2. **打包文件 (主进程):**

   - 你需要 `archiver`：`npm install archiver`。
   - 使用 `dialog.showSaveDialog` 让用户选择保存位置。

   TypeScript

   ```
   // main.ts
   import * as archiver from 'archiver';
   // ... (假设 getEmojisByIds 函数可用，你可以将其添加到 database.ts 中)
   
   // 根据 ID 获取表情包的示例函数 (将其添加到你的数据库函数中)
   export function getEmojisByIds(ids: number[]): Promise<any[]> {
       return new Promise((resolve, reject) => {
           if (ids.length === 0) return resolve([]);
           const placeholders = ids.map(() => '?').join(',');
           db.all(`SELECT name, path FROM emojis WHERE id IN (${placeholders})`, ids, (err, rows) => {
               if (err) reject(err);
               else resolve(rows);
           });
       });
   }
   
   ipcMain.handle('export-emojis', async (event, emojiIds: number[]) => {
       try {
           const emojisToExport = await getEmojisByIds(emojiIds);
           if (emojisToExport.length === 0) return null; // 没有可导出的内容
   
           const saveResult = await dialog.showSaveDialog({
               title: '保存表情包归档',
               defaultPath: `emojis-${Date.now()}.zip`,
               filters: [{ name: 'ZIP Archives', extensions: ['zip'] }]
           });
   
           if (saveResult.canceled || !saveResult.filePath) {
               return null; // 用户取消
           }
   
           const output = fs.createWriteStream(saveResult.filePath);
           const archive = archiver('zip', {
               zlib: { level: 9 } // 最佳压缩
           });
   
           // 处理输出流关闭和错误
           output.on('close', () => {
               console.log(`已创建归档: ${saveResult.filePath} (${archive.pointer()} 总字节)`);
           });
           archive.on('error', (err) => {
               throw err;
           });
   
           archive.pipe(output);
   
           for (const emoji of emojisToExport) {
               const fullPath = path.join(emojiStoragePath, emoji.path);
               if (fs.existsSync(fullPath)) {
                   archive.file(fullPath, { name: emoji.name }); // 将文件添加到归档中，使用其原始名称
               } else {
                   console.warn(`导出文件未找到: ${fullPath}`);
               }
           }
   
           await archive.finalize(); // 完成归档 (这将关闭输出流)
   
           return saveResult.filePath; // 返回保存归档的路径
       } catch (error) {
           console.error('导出表情包错误:', error);
           throw error;
       }
   });
   ```

------



#### 3.4 UI/UX (渲染进程)



这是你选择的前端框架发挥作用的地方。

- **表情包列表组件：**
  - 显示表情包缩略图的网格或瀑布流布局。
  - `<img>` 标签的 `src` 属性使用 `file://` 协议。
  - 如果你预计会有很多表情包，请实现**无限滚动**或**分页**。
  - 为批量操作添加**选择机制**（例如，悬停或点击时的复选框）。
- **搜索/筛选组件：**
  - 用于**文本搜索**（按名称、标签）的输入字段。
  - 用于**按类型**（gif、png）或**标签**筛选的下拉菜单或复选框。
  - 对搜索输入进行防抖处理，以避免过多的 IPC 调用。
- **工具栏组件：**
  - “导入表情包”、“导出选定”、“删除选定”等按钮。
  - 可能还有一个“刷新”按钮。
- **详情/编辑弹窗/模态框：**
  - 点击表情包时，打开一个模态框显示更大的预览。
  - 允许编辑该特定表情包的标签。
  - 显示大小、类型、创建日期等元数据。
- **拖放上传：**
  - 监听指定区域（例如，主窗口或“导入区域”）的 `dragover` 和 `drop` 事件。
  - 在**渲染器**中，获取 `event.dataTransfer.files` 数组。
  - 从每个 `File` 对象中提取 `path` 属性。
  - 通过 `ipcRenderer.invoke('emoji:importFiles', filePaths)` 将这些路径发送到**主进程**。
- **响应式设计：** 使用 CSS Flexbox 或 Grid 进行布局，使其适应不同的窗口大小。

------



### 4. 安全考虑 (预加载脚本的重要性)



你已经强调了 Electron 开发中最重要的安全方面：**绝不能直接将 Node.js API 暴露给渲染进程。**

`preload.ts` 脚本是你的**白名单机制**。 你提供的 `preload.ts` 示例非常完美。对于渲染器需要调用的主进程中的每个函数，都要使用 `contextBridge.exposeInMainWorld` 定义一个相应的暴露函数。

TypeScript

```
// preload.ts
import { contextBridge, ipcRenderer } from 'electron';

contextBridge.exposeInMainWorld('electronAPI', {
    // 渲染器可以在主进程上调用的函数
    openFileDialog: () => ipcRenderer.invoke('dialog:openFile'),
    getEmojis: () => ipcRenderer.invoke('db:getEmojis'),
    addEmoji: (data: any) => ipcRenderer.invoke('db:addEmoji', data),
    deleteEmojis: (ids: number[]) => ipcRenderer.invoke('db:deleteEmojis', ids),
    updateEmojiTags: (id: number, tags: string) => ipcRenderer.invoke('db:updateEmojiTags', id, tags),
    exportEmojis: (ids: number[]) => ipcRenderer.invoke('export-emojis', ids),
    searchEmojis: (query: string) => ipcRenderer.invoke('db:searchEmojis', query),
    getEmojiStoragePath: () => ipcRenderer.invoke('app:getEmojiStoragePath'), // 获取 img src 的基本路径

    // 主进程向渲染器发送更新的机制
    onEmojiUpdate: (callback: (event: any, emojiData: any) => void) => {
        ipcRenderer.on('update-emoji-list', callback);
        return () => { // 返回一个取消订阅函数，用于清理
            ipcRenderer.removeListener('update-emoji-list', callback);
        };
    }
});
```

在你的渲染器中（例如 React 组件的 `useEffect` 或 Vue 的 `mounted` 钩子中），你会使用：

TypeScript

```
// renderer.ts (或 React/Vue 组件文件)
// 获取所有表情包
async function fetchEmojis() {
    const emojis = await window.electronAPI.getEmojis();
    // 使用 emojis 更新你的组件状态
}

// 监听主进程的更新
window.electronAPI.onEmojiUpdate(() => {
    console.log('表情包列表已更新，正在刷新 UI...');
    fetchEmojis(); // 重新获取表情包或更新特定项目
});
```

------



### 5. 打包和发布



Electron Forge 极大地简化了这一过程。

**打包命令：**

Bash

```
npm run make
```

这个命令将：

1. 打包你的应用程序代码。
2. 为你的当前操作系统生成可分发包（例如，Windows 的 `.exe`、macOS 的 `.dmg`、Linux 的 `.deb`/`.rpm`）。
3. 输出将在你项目的 `out/` 目录中。

**配置文件 (`forge.config.js`):** 这个文件由 `electron-forge init` 生成。你可以在这里自定义构建的各个方面：

JavaScript

```
// forge.config.js
module.exports = {
  packagerConfig: {
    // 传递给 electron-packager 的选项
    name: 'My Emoji Manager', // 应用程序名称
    executableName: 'EmojiManager', // 可执行文件名称
    icon: './path/to/your/icon', // .ico (Windows) 或 .icns (macOS) 文件的路径
    appCopyright: 'Your Company Name © 2025',
    asar: true, // 将应用程序打包到 ASAR 存档中，以获得更好的性能/安全性
  },
  rebuildConfig: {},
  makers: [
    {
      name: '@electron-forge/maker-squirrel', // Windows 安装程序
      config: {
        // Squirrel.Windows 的选项
      },
    },
    {
      name: '@electron-forge/maker-zip', // macOS zip
      platforms: ['darwin'],
    },
    {
      name: '@electron-forge/maker-deb', // Debian/Ubuntu Linux
      config: {},
    },
    {
      name: '@electron-forge/maker-rpm', // RedHat/CentOS Linux
      config: {},
    },
  ],
  plugins: [
    {
      name: '@electron-forge/plugin-webpack',
      config: {
        // ... webpack 配置
      },
    },
  ],
};
```

**重要：** 记得将 `'./path/to/your/icon'` 替换为你的应用程序图标文件的实际路径。通常，你需要 Windows 的 `.ico` 文件和 macOS 的 `.icns` 文件。

------



### Electron 开发流程总结：



1. **明确需求和 UI 交互：** 设计你的应用程序界面和功能。
2. **设置 Electron 项目：** 使用 `electron-forge init` 进行初始化。
3. **开发主进程 (`main.ts`):** 实现所有 Node.js 特定的逻辑、文件操作、数据库交互和 IPC 处理器。
4. **开发预加载脚本 (`preload.ts`):** 通过暴露安全 API 的白名单，创建主进程和渲染进程之间的安全桥梁。
5. **开发渲染进程 (`renderer.ts`):** 使用你选择的前端框架构建用户界面，并**只通过预加载脚本暴露的 API** 调用主进程功能。
6. **调试：** 利用 Electron 内置的开发者工具（在开发模式下按 `F12` 或 `Ctrl+Shift+I` 访问）调试渲染器（像浏览器一样）和主进程（Node.js 调试器）。
7. **测试：** 在 Windows、macOS 和 Linux 上彻底测试你的应用程序，以确保跨平台兼容性和功能。
8. **打包发布：** 使用 `npm run make` 和 `forge.config.js` 创建可分发安装程序。

------

这个详细的分解，包括代码片段和每个关键部分的解释，应该能为构建你的 Electron 表情包管理器提供坚实的基础。祝你好运！🚀