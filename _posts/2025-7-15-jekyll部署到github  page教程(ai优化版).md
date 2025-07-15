## **Jekyll 博客部署到 GitHub Pages 并使用 Cloudflare 域名解析的完整教程**



**目标：** 搭建个人博客，实现公网访问，并通过本地推送文档来实现内容更新。

**准备工作：**

- **GitHub 账号** (核心，用于托管代码和 GitHub Pages)
- **域名** (可选，可通过第三方服务商购买或使用免费域名，如 `bailanwa.dpdns.org` 或其他提供商)
- **Cloudflare 账号** (可选，提供 CDN、DDoS 防护和免费 SSL，加速并保护网站)
- **Ruby 环境** (Jekyll 运行所需)
- **Git 工具** (用于本地与远程仓库同步)

------



### **一、创建 GitHub 仓库**



1. 登录 GitHub，点击右上角 `+` 号，选择 `New repository`。
2. **仓库命名规范：**
   - **个人/组织博客：** 仓库名必须是 `你的GitHub用户名.github.io` (例如：`octocat.github.io`)。这是 GitHub Pages 的默认配置方式，无需额外设置分支即可发布。
   - **项目博客：** 仓库名可以是任意项目名（例如 `my-project-blog`）。这种情况下，你的博客将会在 `你的GitHub用户名.github.io/my-project-blog` 下访问。
3. **设置可见性：** 默认是 `Public`，不需要更改，因为 GitHub Pages 只能发布公共仓库。
4. **初始化选项：**
   - 勾选 `Add a README file` (稍后可用于记录自定义域名)。
   - 在 `Add .gitignore` 中选择 `Jekyll`，这将自动生成一个 `.gitignore` 文件，忽略 Jekyll 构建过程中生成的临时文件，避免不必要的提交。
   - 在 `Choose a license` 中选择 `MIT License` (或你喜欢的许可证)。
5. 点击 `Create repository`，新仓库就创建成功了！

------



### **二、本地部署 Jekyll 环境**





#### **1. 安装 Ruby 和 Jekyll**



Jekyll 是一个 Ruby Gem，需要 Ruby 环境来运行。

- **下载 RubyInstaller for Windows：** 访问 https://rubyinstaller.org/downloads/。推荐下载带有 `Devkit` 的最新稳定版本（例如 `Ruby+Devkit x64`）。

- **安装 Ruby：**

  - 运行下载的安装包。
  - **务必勾选 `Add Ruby executables to your PATH` (将 Ruby 可执行文件添加到 PATH 环境变量)，这样你才能在命令行中直接使用 Ruby 命令。**
  - 安装过程中，会提示安装 `MSYS2 Development Toolchain`，请选择安装，这将为你提供编译 Jekyll 依赖所需的工具链。

- **安装 Jekyll 和 Bundler Gem：**

  - 打开命令提示符 (CMD) 或 PowerShell。

  - 输入以下命令安装 Jekyll 和 Bundler：

    Bash

    ```
    gem install jekyll bundler
    ```

- **检查安装：**

  - 输入以下命令检查 Ruby 和 Gem 版本，确认安装成功：

    Bash

    ```
    ruby -v   # 检查 Ruby 版本
    gem -v    # 检查 Gem 版本
    jekyll -v # 检查 Jekyll 版本
    ```

  - 如果显示对应版本号，则表示安装成功。



#### **2. 创建并初始化 Jekyll 站点**



现在，我们将在本地初始化你的 Jekyll 博客。

- **创建博客目录：**

  Bash

  ```
  jekyll new my-blog  # 将 'my-blog' 替换为你的博客目录名，例如 'snxjzaioxk.github.io'
  ```

  这条命令会在当前目录下创建一个新的 Jekyll 站点结构。

- **进入博客目录：**

  Bash

  ```
  cd my-blog # 进入你刚刚创建的博客目录
  ```

- **安装项目依赖：**

  Bash

  ```
  bundle install
  ```

  这条命令会根据项目目录下的 `Gemfile` 安装所有 Jekyll 依赖。



#### **3. 本地预览博客**



**重要：** 确保你始终在你的博客根目录（例如 `my-blog` 或 `snxjzaioxk.github.io`）下运行 Jekyll 命令。

- **启动本地服务器：**

  Bash

  ```
  bundle exec jekyll serve
  ```

- **浏览器访问：** 打开浏览器，访问 `http://localhost:4000`。你应该能看到你的 Jekyll 博客的默认页面。

------



### **三、本地内容更新与网站结构优化**



在开始内容创作前，先优化配置和文件结构，避免后期问题。



#### **1. 配置 `_config.yml` 文件**



`_config.yml` 是博客的全局设置文件。

- **打开你的博客根目录下的 `_config.yml` 文件。**

- **根据你的需求修改以下配置：**

  YAML

  ```
  # 站点基本信息
  title: "Aliom个人博客"       # 网页标题，将显示在浏览器标签页和网站头部
  email: "3442803364@qq.com"  # 替换为你的邮箱地址
  description: "这是Aliom的个人博客，分享技术、生活和学习心得。" # 网站的描述，用于SEO
  
  # URL 配置 (非常重要，影响链接生成)
  baseurl: ""                 # 如果你的 GitHub Pages 仓库名是 '你的GitHub用户名.github.io' (即用户/组织页)，这里留空。
                              # 如果是项目页 (例如 '你的GitHub用户名.github.io/my-blog')，则填写 '/my-blog'。
  url: "https://bailanwa.dpdns.org" # 如果你使用自定义域名，填写自定义域名。如果暂时没有，可以留空或写 GitHub Pages 默认域名。
  github_username: snxjzaioxk # 你的 GitHub 用户名
  
  # 主题和 Markdown 解析器设置
  theme: minima                # 你正在使用的主题名称
  markdown: kramdown           # Markdown 解析器
  highlighter: rouge           # 代码高亮工具
  permalink: pretty            # 文章链接格式，例如 /year/month/day/title/
  
  # 插件
  plugins:
    - jekyll-feed              # RSS 订阅
    - jekyll-seo-tag           # SEO 优化 (建议添加)
    # ... 如果有其他插件，在此处添加
  
  # 字符编码
  encoding: utf-8
  
  # 排除文件 (这些文件不会被 Jekyll 处理和生成)
  exclude:
    - .sass-cache/
    - .jekyll-cache/
    - gemfiles/
    - Gemfile
    - Gemfile.lock
    - node_modules/
    - vendor/bundle/
    - vendor/cache/
    - vendor/gems/
    - vendor/ruby/
    - Rakefile
    - README.md # 如果你不希望 README 被 Jekyll 渲染成页面，则排除
  ```

- **保存 `_config.yml` 文件。**



#### **2. 管理博客文章（Posts）**



博客文章文件位于 `_posts` 文件夹。

- **命名格式：** 必须严格遵循 `YYYY-MM-DD-你的文章标题.md` (或 `.markdown`)。例如：`2025-07-11-my-first-post.md`。标题部分建议使用英文小写字母和连字符。

- **Front Matter：** 每篇文章顶部必须有 Front Matter，包含布局、标题、日期和分类等信息。

  Markdown

  ```
  ---
  layout: post
  title: "我的第一篇博客文章"
  date: 2025-07-11 10:00:00 +0800 # 日期和时间，+0800 是时区偏移
  categories: [生活, 学习] # 可选：文章分类
  tags: [Jekyll, 入门] # 可选：文章标签
  ---
  这是我的第一篇博客文章内容。你可以在这里开始你的写作。
  这是文章的剩余部分，只有点击文章标题才能看到。
  ```



#### **3. 添加和管理页面（Pages）**



页面是独立于文章的静态内容，例如“关于我”、“日常生活”、“联系方式”等。

- **创建页面文件：** 在博客根目录 (`my-blog/`) 下创建 Markdown 或 HTML 文件，例如 `about.md`, `daily-life.md`, `contact.md`, `archive.md`。

- **Front Matter：** 页面文件也需要 Front Matter。

  - **示例 (`about.md`):**

    Markdown

    ```
    ---
    layout: page # 使用 'page' 布局，如果你的主题没有，则用 'default'
    title: 关于我 # 页面标题
    permalink: /about/ # 页面的 URL，访问时为 yourdomain.com/about/
    ---
    # 关于我
    
    你好，我是 Aliom！...
    ```

- **现有页面优化：**

  - **`index.md`：**

    Markdown

    ```
    ---
    layout: home # 如果你的主题提供 home 布局，或者 default
    title: 首页
    ---
    ```

  - **`archive.md` (文章归档)：** 这个文件负责列出所有文章和分类。

    Markdown

    ```
    ---
    layout: page
    title: 文章归档
    permalink: /archive/
    ---
    <h1>文章归档</h1>
    <h2>所有分类</h2>
    {% assign categories_list = site.categories | sort %}
    {% for category in categories_list %}
      <a href="#{{ category[0] | slugify: 'pretty' }}" class="category-link">{{ category[0] }} ({{ category[1].size }})</a> &nbsp; 
    {% endfor %}
    <hr>
    {% for category in site.categories %}
      <h3 id="{{ category[0] | slugify: 'pretty' }}">{{ category[0] }}</h3> 
      <ul>
        {% for post in category[1] %}
          <li>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a> - {{ post.date | date: "%Y年%m月%d日" }}
          </li>
        {% endfor %}
      </ul>
    {% endfor %}
    ```



#### **4. 图片管理与引用**



为了确保图片在本地和线上都能正确加载，统一管理和正确引用非常重要。

- **创建图片目录：** 在博客根目录创建 `assets/images/` 文件夹（如果不存在）。

- **放置图片：** 将你的图片文件（例如 `my-image.png`）复制到 `assets/images/` 目录下。

- **正确引用图片：** **切勿使用本地文件系统路径**（例如 `C:\Users\Aliom\...`）。

  - **Markdown 语法：**

    Markdown

    ```
    ![图片描述]( {{ "/assets/images/my-image.png" | relative_url }} "可选标题")
    ```

  - **HTML 语法 (用于高级控制，如设置尺寸)：**

    HTML

    ```
    <img src="{{ "/assets/images/my-image.png" | relative_url }}" alt="图片描述" width="500px" style="zoom:67%;">
    ```

  - **关键：** `"/assets/images/my-image.png"` 是相对于你博客网站根目录的路径，`| relative_url` 过滤器会自动处理 `baseurl`。确保文件名和目录名与 GitHub 上的一致，包括**大小写**。



#### **5. 优化布局文件 (`_layouts/default.html` 或 `_layouts/home.html`)**



布局文件定义了页面和文章的整体结构。

- **打开 `_layouts/default.html` 或 `_layouts/home.html`。**

- **`<title>` 标签：** 使用 `{{ page.title | default: site.title | escape }}`，这会优先显示当前页面的标题，如果没有定义，则显示 `_config.yml` 中的站点标题。

- **内容主体：** 在 `<main>` 标签内部，使用 `{{ content }}` 来动态插入各个页面或文章的具体内容。

- **导航菜单：** 确保导航链接指向正确的页面 URL。

  HTML

  ```
  <nav class="site-nav">
      <a href="{{ "/" | relative_url }}">我的博客主页</a>
      <a href="{{ "/about/" | relative_url }}">关于我</a>
      <a href="{{ "/archive/" | relative_url }}">文章归档</a>
      <a href="{{ "/daily-life/" | relative_url }}">日常生活</a>
      <a href="{{ "/contact/" | relative_url }}">联系方式</a>
  </nav>
  ```

- **保存布局文件。**



#### **6. 本地再次预览博客**



每次进行重大修改后，都应该在本地进行预览，确保一切正常。

- **停止当前 Jekyll 服务器** (`Ctrl + C`)。
- **清理缓存**：`bundle exec jekyll clean`
- **重新启动**：`bundle exec jekyll serve`
- 访问 `http://localhost:4000`，仔细检查所有页面和功能。

------



### **四、将本地仓库推送至 GitHub 仓库**



这是将你的本地博客部署到 GitHub Pages 的核心步骤。



#### **准备工作：安装 Git 工具**



- **下载 Git：** 访问 https://git-scm.com/downloads。
- **安装 Git：** 按照安装向导进行，**确保在安装过程中勾选 `Use Git from the Windows Command Prompt` 或 `Git from the command line and also from 3rd-party software`，这样 Git 才能添加到系统 PATH 环境变量中。**



#### **Git 操作命令**



在你的博客根目录（例如 `my-blog` 或 `snxjzaioxk.github.io`）中打开命令行。

1. **初始化 Git 仓库 (如果你的目录还不是 Git 仓库)：**

   Bash

   ```
   git init
   ```

2. **关联远程仓库：** 将本地仓库与你在第一步创建的 `你的用户名.github.io` 远程仓库关联。

   Bash

   ```
   git remote add origin https://github.com/你的用户名/你的GitHub用户名.github.io.git
   # 将 '你的用户名' 替换为你的实际 GitHub 用户名
   ```

   - **如果已关联过，出现 `fatal: remote origin already exists` 错误：** 可以先移除旧的关联：`git remote rm origin`，然后重新添加。

3. **暂存所有文件：**

   Bash

   ```
   git add .
   ```

4. **提交更改：**

   Bash

   ```
   git commit -m "Initial Jekyll blog setup and content optimization"
   ```

   - **提示：** `git commit -m "Your commit message"`， `-m` 后面的字符串是提交信息。

5. **将主分支重命名为 `main` (如果不是)：** GitHub 默认分支现在是 `main`，如果你的本地默认是 `master`，执行：

   Bash

   ```
   git branch -M main
   ```

6. **推送到 GitHub：**

   Bash

   ```
   git push origin main
   ```



#### **解决 `git push` 失败问题 (网络连接问题)**



如果 `git push` 失败，出现 `Failed to connect to github.com port 443` 或 `Connection was reset` 等错误，通常是网络或代理问题。

- **方法一：取消 Git 的全局代理设置 (推荐优先尝试)**

  Bash

  ```
  git config --global --unset http.proxy
  git config --global --unset https.proxy
  ```

  它们的作用是移除 Git 的全局 HTTP 和 HTTPS 代理配置，让 Git 直接尝试连接远程服务器。

- **方法二：临时禁用防火墙/杀毒软件** Windows Defender 或第三方杀毒软件有时会拦截 Git 的 HTTPS 连接。

- **方法三：临时禁用系统代理/VPN** 确保没有系统级的代理设置或 VPN 在运行。

- **方法四：切换网络环境** 尝试连接手机热点或在其他网络环境下进行 `git push`，以排除当前网络的限制。

- **方法五：更改 Git 的 SSL 后端** 有时 Windows 上的 Git 默认 OpenSSL 后端会有问题，可以尝试切换到 SChannel。

  Bash

  ```
  git config --global http.sslBackend schannel
  ```

- **方法六：设置 Git 使用本地代理 (高级)** 如果你有本地运行的代理软件（如 Clash, V2Ray 等），并且端口是 `7890`，可以尝试：

  Bash

  ```
  git config --global http.proxy http://127.0.0.1:7890
  git config --global https.proxy http://127.0.0.1:7890 # HTTPS 也需要设置
  ```

  设置完成后，可以通过 `git config --global -l` 检验是否设置成功。 **注意：** 如果你的代理需要认证，或者端口不是 `7890`，请根据实际情况修改。



### **五、配置 GitHub Pages**



一旦代码成功推送到 GitHub，你需要在仓库设置中启用 GitHub Pages。

1. **进入你的 GitHub 仓库** (例如 `snxjzaioxk/snxjzaioxk.github.io`)。
2. 点击顶部的 `Settings` (设置) 选项卡。
3. 在左侧导航栏中，点击 `Pages`。
4. 在 "`Source`" 部分：
   - 选择你的 **构建分支** (通常是 `main`)。
   - 选择 **文件夹** (`/(root)`)。
   - **重要：** 暂时**不要**在 GitHub Pages 设置中填写 "`Custom domain`" (自定义域名) 部分。这一步将由 Cloudflare 处理。
5. 点击 `Save` (保存)。
6. GitHub Pages 会开始构建你的网站。在这一步，你的网站应该可以通过 `https://你的GitHub用户名.github.io` 或 `https://你的GitHub用户名.github.io/你的项目名称` 访问。



### **六、将域名添加到 Cloudflare**



如果你有自定义域名，并希望通过 Cloudflare 来管理 DNS 和获得其优势。

1. **购买域名：** 确保你已经从域名注册商处购买了一个域名（例如 `yourdomain.com`）。
2. **注册 Cloudflare 账号：** 访问 https://www.cloudflare.com/ 注册并登录。
3. **添加你的网站 (域名)：**
   - 登录 Cloudflare 仪表盘，点击 "`Add site`" (添加站点) 按钮。
   - 在输入框中，**精确输入你的自定义域名**（例如 `yourdomain.com`，不要带 `www.` 或 `http/https://`）。
   - 点击 "`Add site`" (添加站点)。
   - 选择 "`Free`" 计划，然后点击 "`Continue`" (继续)。
   - Cloudflare 会自动扫描你域名现有的 DNS 记录。



### **七、Cloudflare 域名解析配置**



这是将你的自定义域名指向 GitHub Pages 的核心。

1. **更改域名 DNS 服务器 (NS 服务器)：**
   - 登录你的**域名注册商**（例如 GoDaddy, Namecheap, 阿里云等）的网站。
   - 找到你的域名管理界面，将 **DNS 服务器 (或 NS 服务器)** 修改为 Cloudflare 提供的 DNS 服务器。Cloudflare 在你添加域名后会给你具体的服务器地址（通常是两个以 `cloudflare.com` 结尾的地址）。
   - **这一步是让 Cloudflare 接管你的域名解析权。** DNS 更改可能需要几分钟到几小时才能全球生效。
2. **在 Cloudflare 中添加 DNS 记录：**
   - 登录 Cloudflare 账号，选择你的域名，然后点击 "`DNS`" 选项卡。
   - **添加记录：**
     - **如果你的 GitHub Pages 仓库是用户/组织主页 (即 `snxjzaioxk.github.io`)，并希望使用裸域名 (yourdomain.com)：** 添加 **四条 A 记录**，指向 GitHub Pages 的 IP 地址。这些 IP 地址可能会有变动，建议查询 GitHub Pages 官方文档获取最新。目前常见的 IP 是：
       - `185.199.108.153`
       - `185.199.109.153`
       - `185.199.110.153`
       - `185.199.111.153` 配置示例： `Type: A`, `Name: @`, `Content: 185.199.108.153`, `Proxy status: Proxied (橙色云朵)` (重复四次，分别填入上述四个 IP)
     - **如果你的 GitHub Pages 仓库是用户/组织主页，并希望使用 `www` 子域名 (`www.yourdomain.com`)：** 添加 **一条 CNAME 记录**： `Type: CNAME`, `Name: www`, `Content: snxjzaioxk.github.io`, `Proxy status: Proxied (橙色云朵)`
       - **注意：** `snxjzaioxk.github.io` 是你的 GitHub Pages 默认域名，请替换为你的实际 GitHub Pages 域名。
     - **如果你的 GitHub Pages 仓库是项目页 (例如 `snxjzaioxk.github.io/my-blog`)：** 通常只使用 CNAME 记录。 `Type: CNAME`, `Name: www`, `Content: snxjzaioxk.github.io`, `Proxy status: Proxied (橙色云朵)`
       - **这里的 `Content` 仍然是你的 `username.github.io`，而不是 `username.github.io/repo-name`。GitHub 会根据你仓库中的 `CNAME` 文件自动重定向。**
   - **`Proxy status` (橙色云朵)：** 确保所有指向你博客的 DNS 记录都显示为橙色云朵，这意味着你的网站流量将通过 Cloudflare 的 CDN 和安全服务。



#### **3. Cloudflare SSL/TLS 设置 (强烈推荐)**



Cloudflare 提供免费的 SSL 证书，确保你的网站使用 HTTPS 访问。

1. 在 Cloudflare 仪表盘中，点击 "`SSL/TLS`" -> "`Overview`"。
2. 确保 "`SSL/TLS encryption mode`" 设置为 **`Full`** 或 **`Full (strict)`**。
   - `Full`：访客到 Cloudflare (HTTPS)，Cloudflare 到你的源服务器 (GitHub Pages) (HTTPS，Cloudflare 验证 GitHub Pages 证书)。
   - `Full (strict)`：更严格，要求源服务器的 SSL 证书是可信的。对于 GitHub Pages，通常 `Full` 就足够了。
3. 点击 "`Edge Certificates`" 选项卡。
4. 开启 "`Always Use HTTPS`"：这将强制所有 HTTP 请求自动重定向到 HTTPS。
5. 开启 "`Automatic HTTPS Rewrites`"：这将尝试将页面内容中的 HTTP 链接自动重写为 HTTPS。



#### **4. 完成自定义域名设置**



1. **在本地博客根目录创建 `CNAME` 文件：** 创建名为 `CNAME` 的**纯文本文件**（没有文件扩展名），并在其中**只写入你的自定义域名**。

   - 如果你希望使用 `www.yourdomain.com`，内容就是 `www.yourdomain.com`。
   - 如果你希望使用裸域名 `yourdomain.com`，内容就是 `yourdomain.com`。
   - **注意：** 文件中只有一行域名，没有其他内容或空白行。

2. **将 `CNAME` 文件推送到 GitHub：**

   Bash

   ```
   git add CNAME
   git commit -m "Add CNAME file for custom domain"
   git push origin main
   ```

3. **等待 DNS 生效并测试：** DNS 记录的更改和 Cloudflare 的配置生效可能需要几分钟到几小时。你可以使用在线 DNS 查询工具（如 `dnschecker.org`）来检查你的域名是否已正确解析到 Cloudflare 和 GitHub Pages。

4. **访问你的自定义域名：** 在浏览器中输入你的自定义域名（例如 `https://www.yourdomain.com` 或 `https://yourdomain.com`），确认博客可以正常访问。



### **八、补充及注意事项**



- **Jekyll 命令行安装路径：** 默认路径通常是 `C:\Users\用户\你的博客目录名`。通常不需要更改，更改路径可能需要重新配置环境变量或 Git 仓库路径。
- **`_site` 文件夹：** 这是 Jekyll 自动化部署时生成的静态网站文件，不需要手动管理或推送到 Git 仓库（`.gitignore` 已经帮你忽略了）。
- **根目录下 `index.md`：** 作为博客的主页文件，这是必须的。
- **Jekyll 插件：** 如果你使用了额外的 Jekyll 插件，确保它们已添加到 `_config.yml` 的 `plugins` 列表中，并且在本地通过 `bundle install` 安装。
- **性能优化：**
  - **图片大小：** 不建议上传过大的图片，会影响页面加载速度。考虑使用图片压缩工具或使用 WebP 等现代化图片格式。
  - **CSS/JS 优化：** 如果你的主题没有内置，可以考虑 CSS 和 JavaScript 的压缩和合并。
  - **Cloudflare Page Rules：** Cloudflare 提供了 Page Rules 功能，可以进行更高级的缓存、重定向等优化设置。

本教程涵盖了部署 Jekyll 博客到 GitHub Pages 并使用 Cloudflare 进行域名解析的全部关键步骤。希望对你建立和维护个人博客有所帮助！