### 方案一：纯本地桌面应用 (Electron) 详细指南

**核心思想：** 利用 Electron 将 Web 前端 (HTML/CSS/JS) 技术打包成一个可以在 Windows、macOS 和 Linux 上运行的桌面应用程序。这样，你可以利用前端开发经验来构建用户界面，同时拥有 Node.js 的能力来访问本地文件系统和 SQLite 数据库。

------

#### 1. 技术栈选择与环境搭建

- **前端框架 (可选但推荐):** React, Vue, Angular, Svelte。这些框架能帮助你更好地组织和管理 UI 组件，提高开发效率。如果你是初学者，也可以先从纯 HTML/CSS/JS 开始。
- **后端/桌面层:** Electron (内置 Chromium 和 Node.js)。
- **数据库:** SQLite (轻量级，文件型数据库，无需独立服务器)。
- **其他工具:**
  - `npm` 或 `yarn` (包管理器)
  - `electron-forge` (Electron 官方推荐的开发工具，用于快速初始化项目、打包和发布)

**环境搭建步骤：**

1. **安装 Node.js：** 访问 [nodejs.org](https://nodejs.org/) 下载并安装 LTS 版本。Node.js 会自带 `npm`。

2. **安装 Electron Forge：**

   ```
   bash
   
   
   复制
   npm install -g electron-forge
   ```

3. **创建新项目：**

   ```
   bash复制electron-forge init my-emoji-manager --template=webpack-typescript # 或 --template=webpack (如果你不用TypeScript)
   cd my-emoji-manager
   npm start # 启动开发模式
   ```

   这会创建一个基本的 Electron 项目结构，并自动安装好所有依赖。

------

#### 2. 项目结构详解 (Electron 示例)

```
perl复制my-emoji-manager/
├── package.json           # 项目配置，依赖，脚本
├── forge.config.js        # Electron Forge 配置，用于打包
├── src/
│   ├── main.ts            # Electron 主进程代码 (Node.js 环境)
│   ├── preload.ts         # 预加载脚本 (安全桥接主进程和渲染进程)
│   ├── renderer.ts        # 渲染进程入口 (你的前端代码)
│   ├── index.html         # 渲染进程的 HTML 模板
│   ├── assets/            # (你自己创建) 用于存放管理的表情包文件
│   └── database/          # (你自己创建) 用于存放 SQLite 数据库文件 (比如 emoji.db)
├── .gitignore
└── README.md
```

- **`main.ts` (主进程):**
  - 负责创建和管理浏览器窗口。
  - 处理文件系统操作 (读、写、删除、复制文件)。
  - 与 SQLite 数据库交互 (查询、插入、更新、删除数据)。
  - 监听渲染进程发来的请求 (IPC 通信)。
  - 使用 Node.js 内置模块 (`fs`, `path`, `sqlite3` 等)。
- **`preload.ts` (预加载脚本):**
  - 在渲染进程加载之前运行，拥有 Node.js 环境的访问权限。
  - **重要！** 它是连接主进程和渲染进程的**安全桥梁**。不要直接在渲染进程中暴露 Node.js API。通过 `contextBridge` 暴露一个安全的 API 给渲染进程。
- **`renderer.ts` (渲染进程):**
  - 你的前端 UI 代码 (React/Vue/纯JS)。
  - 通过 `preload.ts` 暴露的 API 与主进程通信，发送请求 (例如“扫描表情包”、“删除表情包”)。
  - 负责渲染表情包列表、搜索框、筛选器等。
- **`assets/`:** 存放用户导入的表情包文件。
- **`database/`:** 存放 SQLite 数据库文件 (例如 `emoji.db`)。

------

#### 3. 核心功能模块实现细节

##### 3.1 数据存储 (SQLite)

- **数据库文件位置：** 推荐放在用户数据目录，或者应用安装目录下的一个子文件夹（例如 `my-emoji-manager/data/emoji.db`）。

- **表设计示例：**

  ```
  sql复制CREATE TABLE IF NOT EXISTS emojis (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      name TEXT NOT NULL,         -- 文件名，例如 "happy_cat.gif"
      path TEXT NOT NULL UNIQUE,  -- 在 assets 文件夹内的相对路径
      size INTEGER,               -- 文件大小 (字节)
      type TEXT,                  -- 文件类型 (gif, png, jpg, webp)
      tags TEXT,                  -- 标签，可以存储为逗号分隔的字符串或 JSON 数组
      created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
      last_used_at DATETIME       -- (可选) 记录使用频率
  );
  ```

- **SQLite 库：** 在主进程中使用 `sqlite3` (或 `better-sqlite3`，性能更好) 这个 npm 包来操作数据库。

  ```
  bash复制npm install sqlite3 # 或 npm install better-sqlite3
  npm install @types/sqlite3 # 如果使用 TypeScript
  ```

  **主进程 (main.ts) 中数据库操作示例：**

  ```
  typescript复制import { app } from 'electron';
  import * as path from 'path';
  import sqlite3 from 'sqlite3'; // 或 'better-sqlite3'
  
  const dbPath = path.join(app.getPath('userData'), 'database', 'emojis.db'); // 推荐放用户数据目录
  let db: sqlite3.Database;
  
  function initDatabase() {
      // 确保数据库目录存在
      require('fs').mkdirSync(path.dirname(dbPath), { recursive: true });
  
      db = new sqlite3.Database(dbPath, (err) => {
          if (err) {
              console.error('Could not connect to database', err);
          } else {
              console.log('Connected to SQLite database.');
              db.run(`
                  CREATE TABLE IF NOT EXISTS emojis (
                      id INTEGER PRIMARY KEY AUTOINCREMENT,
                      name TEXT NOT NULL,
                      path TEXT NOT NULL UNIQUE,
                      size INTEGER,
                      type TEXT,
                      tags TEXT,
                      created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
                      last_used_at DATETIME
                  );
              `, (createErr) => {
                  if (createErr) console.error('Error creating table', createErr);
              });
          }
      });
  }
  
  // 示例：插入表情包
  function insertEmoji(emojiData: { name: string, path: string, size: number, type: string, tags?: string }) {
      return new Promise((resolve, reject) => {
          db.run(`INSERT INTO emojis (name, path, size, type, tags) VALUES (?, ?, ?, ?, ?)`,
              [emojiData.name, emojiData.path, emojiData.size, emojiData.type, emojiData.tags || ''],
              function(err) {
                  if (err) {
                      reject(err);
                  } else {
                      resolve(this.lastID); // 返回新插入的 ID
                  }
              }
          );
      });
  }
  
  // 示例：查询所有表情包
  function getAllEmojis() {
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
  
  // 启动时调用
  app.on('ready', initDatabase);
  ```

##### 3.2 表情包文件管理

**核心：主进程通过 `fs` (Node.js 文件系统模块) 进行文件操作。**

- **约定表情包存储路径：**
   在主进程中定义一个路径，例如 `path.join(app.getPath('userData'), 'emojis')`。

  ```
  typescript复制// main.ts
  const emojiStoragePath = path.join(app.getPath('userData'), 'emojis');
  // 确保目录存在
  require('fs').mkdirSync(emojiStoragePath, { recursive: true });
  ```

- **扫描/导入表情包：**

  1. **用户操作 (渲染进程):** 用户点击“导入”按钮，或拖拽文件到应用界面。

  2. **选择文件/文件夹 (主进程):**

     - 使用 `dialog.showOpenDialog` 让用户选择文件或文件夹。
     - 将文件路径通过 IPC 发送给主进程。

     ```
     typescript复制// preload.ts (暴露给渲染进程的API)
     contextBridge.exposeInMainWorld('electronAPI', {
         openFileDialog: () => ipcRenderer.invoke('dialog:openFile'),
         // ... 其他 API
     });
     
     // main.ts (监听渲染进程的请求)
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

     - 遍历选中的 `filePaths`。
     - 对每个文件：
       - 读取文件信息 (`fs.statSync`)，获取大小。
       - 生成新的文件名 (可使用 UUID 或原始文件名加上时间戳，避免冲突)。
       - 将文件复制到 `emojiStoragePath` (`fs.copyFileSync`)。
       - 将表情包的元数据 (新路径、名称、大小、类型) 插入到 SQLite 数据库。
       - （可选）如果导入的是文件夹，递归扫描文件夹内的图片文件。

- **预览：**

  - 渲染进程接收到表情包数据 (包含在 `emoji.path` 字段)。
  - 在 HTML 中使用 `<img src="file://${emojiStoragePath}/${emoji.path}" />` 直接引用本地文件路径。Electron 默认支持 `file://` 协议。

- **添加/删除/修改：**

  - **删除：**
    1. **用户操作 (渲染进程):** 选择一个或多个表情包，点击删除。
    2. **发送请求 (渲染进程):** 通过 IPC 向主进程发送要删除的表情包 ID 列表。
    3. **执行删除 (主进程):**
       - 根据 ID 从数据库查询出表情包的 `path`。
       - 使用 `fs.unlinkSync(fullPath)` 删除文件。
       - 从 SQLite 数据库中删除对应记录。
       - （可选）通知渲染进程更新列表。
  - **添加/修改标签：**
    1. **用户操作 (渲染进程):** 在 UI 上编辑标签。
    2. **发送请求 (渲染进程):** 通过 IPC 向主进程发送表情包 ID 和新标签内容。
    3. **更新数据库 (主进程):** 更新 SQLite 数据库中对应表情包的 `tags` 字段。

- **搜索/筛选：**

  - **用户操作 (渲染进程):** 输入关键词，选择筛选条件 (如按标签、按类型)。
  - **发送请求 (渲染进程):** 通过 IPC 发送查询参数给主进程。
  - **执行查询 (主进程):** 构建 SQL 查询语句，例如 `SELECT * FROM emojis WHERE name LIKE ? OR tags LIKE ? ORDER BY ...`，从 SQLite 数据库中查询符合条件的表情包。
  - **返回结果 (主进程):** 将查询结果发送回渲染进程，渲染进程更新 UI。

- **批量处理：**

  - 前端 UI 提供多选功能 (例如复选框)。
  - 用户选中多个表情包后，点击“批量删除”或“批量添加标签”等按钮。
  - 渲染进程收集所有选中表情包的 ID，然后一次性通过 IPC 发送给主进程。
  - 主进程接收到 ID 列表后，循环执行删除文件和数据库记录，或批量更新数据库记录。

##### 3.3 导出功能

- **用户操作 (渲染进程):** 选中要导出的表情包，点击“导出”按钮。

- **发送请求 (渲染进程):** 将选中表情包的 ID 列表发送给主进程。

- **打包文件 (主进程):**

  - 使用 `archiver` 等 npm 包（需要安装：`npm install archiver`）来创建 ZIP 文件。
  - 根据 ID 从数据库获取表情包的完整路径。
  - 将这些文件添加到 ZIP 压缩包中。
  - 使用 `dialog.showSaveDialog` 让用户选择保存 ZIP 文件的位置。
  - 将 ZIP 文件写入用户指定的位置。

  ```
  typescript复制// main.ts (部分示例，需要结合 archiver 完整使用)
  import * as archiver from 'archiver';
  import * as fs from 'fs';
  // ... 其他导入
  
  ipcMain.handle('export-emojis', async (event, emojiIds: number[]) => {
      try {
          const emojisToExport = await getEmojisByIds(emojiIds); // 假设你有一个函数根据ID查询表情包
          if (emojisToExport.length === 0) return null;
  
          const savePath = await dialog.showSaveDialog({
              title: '保存表情包',
              defaultPath: `emojis-${Date.now()}.zip`,
              filters: [{ name: 'ZIP Archives', extensions: ['zip'] }]
          });
  
          if (savePath.canceled || !savePath.filePath) {
              return null;
          }
  
          const output = fs.createWriteStream(savePath.filePath);
          const archive = archiver('zip', {
              zlib: { level: 9 } // 最佳压缩
          });
  
          archive.pipe(output);
  
          for (const emoji of emojisToExport) {
              const fullPath = path.join(emojiStoragePath, emoji.path);
              if (fs.existsSync(fullPath)) {
                  archive.file(fullPath, { name: emoji.name }); // 将文件添加到压缩包
              }
          }
  
          await archive.finalize(); // 完成压缩
  
          return savePath.filePath;
      } catch (error) {
          console.error('Error exporting emojis:', error);
          throw error;
      }
  });
  ```

##### 3.4 UI/UX (渲染进程)

- **前端框架：** 如果使用 React/Vue，可以创建组件来管理：
  - **表情包列表组件：** 负责渲染表情包缩略图，支持瀑布流布局。
  - **搜索/筛选组件：** 输入框、标签选择器。
  - **工具栏组件：** 导入、导出、批量删除等按钮。
  - **详情/编辑弹窗：** 显示表情包详情，编辑标签。
- **拖拽上传：** 在渲染进程中监听 `dragover` 和 `drop` 事件，将拖拽的文件路径通过 IPC 发送给主进程进行处理。
- **响应式设计：** 确保界面在不同窗口大小下都能良好显示。

------

#### 4. 安全考虑 (Preload 脚本的重要性)

- **绝不能在渲染进程中直接暴露 Node.js API！** 这是 Electron 的一个主要安全漏洞。

- `preload.ts` 的作用就是创建一个安全的桥梁。

- 通过 `contextBridge.exposeInMainWorld('apiName', { ... })` 方法，你可以定义一个白名单，只暴露你需要的功能给渲染进程。

  ```
  typescript复制// preload.ts
  import { contextBridge, ipcRenderer } from 'electron';
  
  contextBridge.exposeInMainWorld('electronAPI', {
      // 暴露一个函数，用于触发文件对话框
      openFileDialog: () => ipcRenderer.invoke('dialog:openFile'),
      // 暴露一个函数，用于获取所有表情包
      getEmojis: () => ipcRenderer.invoke('db:getEmojis'),
      // 暴露一个函数，用于添加表情包数据到数据库
      addEmoji: (data: any) => ipcRenderer.invoke('db:addEmoji', data),
      // 暴露一个函数，用于删除表情包 (文件和数据库记录)
      deleteEmojis: (ids: number[]) => ipcRenderer.invoke('db:deleteEmojis', ids),
      // 暴露一个函数，用于更新表情包标签
      updateEmojiTags: (id: number, tags: string) => ipcRenderer.invoke('db:updateEmojiTags', id, tags),
      // 暴露一个函数，用于导出表情包
      exportEmojis: (ids: number[]) => ipcRenderer.invoke('export-emojis', ids),
  
      // 你还可以提供一个从主进程接收更新的机制
      onEmojiUpdate: (callback: (event: any, emojiData: any) => void) => ipcRenderer.on('update-emoji-list', callback)
  });
  ```

  这样，在渲染进程中，你只能通过 `window.electronAPI.openFileDialog()` 等方式来调用主进程的功能，而不是直接访问 `fs` 或 `path`。

------

#### 5. 打包和发布

使用 Electron Forge 可以非常方便地打包你的应用。

1. **打包命令：**

   ```
   bash
   
   
   复制
   npm run make
   ```

   这会在 `out/` 目录下生成针对你的操作系统的安装包（例如 `.exe` for Windows, `.dmg` for macOS, `.deb`/`.rpm` for Linux）。

2. **配置文件 (`forge.config.js`):** 你可以在这里配置打包选项，例如应用图标、名称、版权信息等。

------

**总结 Electron 开发流程：**

1. **确定需求和 UI 交互：** 设计你的应用界面。
2. **设置 Electron 项目：** 使用 Electron Forge 初始化。
3. **开发主进程 (`main.ts`):** 处理所有需要 Node.js 能力的逻辑（文件操作、数据库交互、IPC 监听）。
4. **开发预加载脚本 (`preload.ts`):** 作为主进程和渲染进程之间的安全桥梁，只暴露必要的 API 给渲染进程。
5. **开发渲染进程 (`renderer.ts`):** 构建用户界面，通过预加载脚本暴露的 API 调用主进程功能。
6. **调试：** 使用 Electron 内置的开发者工具 (类似 Chrome 开发者工具) 进行调试。
7. **测试：** 在不同操作系统上测试。
8. **打包发布。**