## 准备工作



在开始之前，请确保您已拥有以下资源和工具：

- **GitHub 账号**：这是核心，您的博客将托管在这里。
- **域名**（可选）：您可以选择免费域名或购买自己的域名。
- **Cloudflare 账号**（可选）：它提供 CDN、DDoS 防护和免费 SSL 证书，能优化您的博客性能和安全性。
- **Ruby**：Jekyll 运行所必需的环境。
- **Git 工具**：用于本地代码推送到远程仓库。

------



## 一. 创建 GitHub 仓库



1. **仓库命名**：您的仓库名必须是 `您的GitHub用户名.github.io` (例如：`octocat.github.io`)。
2. **可见性**：默认情况下仓库是 `Public`，无需更改。
3. **初始化设置**：
   - 勾选 **Add a README file**。
   - 在 **Add .gitignore** 中选择 `Jekyll`。
   - 在 **Choose a license** 中选择 `MIT License`。
4. 点击 **Create repository**，您的新仓库就创建成功了！

------



## 二. 本地部署 Jekyll 环境





### 1. 安装 Ruby 和 Jekyll



1. **下载 Ruby**：访问 [RubyInstaller Downloads](https://rubyinstaller.org/downloads/)，下载并安装适合您系统的 Ruby 版本。

2. **安装 Jekyll 和 Bundler**：安装 Ruby 后，打开命令行提示符（CMD 或 PowerShell），输入以下命令并回车：

   Bash

   ```
   gem install jekyll bundler
   ```

3. **检查版本**：安装完成后，可以通过以下命令检查 Ruby 和 Gem 的版本：

   Bash

   ```
   ruby -v
   gem -v
   ```

   如果显示对应版本号，说明安装成功。

4. **创建新站点**：在您希望存放博客的目录下，执行以下命令来建立新的 Jekyll 站点：

   Bash

   ```
   jekyll new my-blog  # 将 my-blog 替换为您的博客目录名
   cd my-blog
   bundle install
   ```



### 2. 本地预览博客



**重要提示**：请确保您已进入 `my-blog` 目录，然后运行以下命令：

Bash

```
bundle exec jekyll serve
```

运行成功后，您可以在浏览器中访问 `http://127.0.0.1:4000` 或命令行中显示的地址，预览您的博客。

------



## 三. 内容更新与配置





### 1. 配置 `_config.yml` 文件



`_config.yml` 是 Jekyll 博客的核心配置文件。请根据您的需求修改以下内容：

YAML

```
title: "Aliom个人博客" # 网页标题
email: 3442803364@qq.com # 替换为您的邮箱地址
description: "" # 描述您的网站

baseurl: "" # 如果没有自定义域名，请留空。如果有自定义域名，则填写 /项目名（如果您的仓库是项目仓库，如 `yourusername.github.io/my-blog`）或留空（如果是用户或组织仓库 `yourusername.github.io`）。
url: "https://bailanwa.dpdns.org" # 填写您的自定义域名（如果使用了）。
github_username: snxjzaioxk # 您的 GitHub 用户名

# 主题设置 - 这是关键
theme: minima

markdown: kramdown
highlighter: rouge
permalink: pretty

plugins:
  - jekyll-feed

encoding: utf-8

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
```



### 2. 添加文章



在 `_posts` 文件夹下添加 Markdown 文件即可新增文章。请务必遵守命名规范：`年份-月份-日期-name.md` (例如：`2025-07-11-my-first-post.md`)。

------



## 四. 将本地仓库推送到 GitHub





### 1. 安装 Git 工具



如果尚未安装，请从 [Git 官方网站](https://git-scm.com/downloads) 下载并安装 Git。



### 2. 推送步骤



1. **初始化 Git 仓库**：如果您的 `my-blog` 目录还没有 Git 仓库，需要先初始化：

   Bash

   ```
   git init
   ```

2. **关联远程仓库**：将本地仓库与您在第一步创建的 `您的用户名.github.io` 远程仓库关联：

   Bash

   ```
   git remote add origin https://github.com/您的用户名/您的用户名.github.io.git
   # 请将 您的用户名 替换为您的实际 GitHub 用户名
   ```

3. **添加所有文件并提交**：

   Bash

   ```
   git add .
   git commit -m "Initial Jekyll blog setup"
   ```

4. **推送到 GitHub**：

   Bash

   ```
   git branch -M main # 将主分支重命名为 main (如果不是)
   git push origin main
   ```



### 3. 解决推送问题



- **移除代理设置**：如果推送失败，可以尝试移除 Git 的全局 HTTP 和 HTTPS 代理配置：

  Bash

  ```
  git config --global --unset http.proxy
  git config --global --unset https.proxy
  ```

- **设置系统代理**：如果移除代理后仍有问题，可以尝试设置 Git 使用本地代理。假设您的代理服务器端口为 `7890`：

  Bash

  ```
  git config --global http.proxy http://127.0.0.1:7890
  ```

  您可以通过 `git config --global -l` 命令来检验是否设置成功。

------



## 五. 配置 GitHub Pages



一旦代码推送到 GitHub，您需要在仓库设置中启用 GitHub Pages。

1. **进入仓库设置**：访问您的 GitHub 仓库 (例如 `my-blog` 或 `yourusername.github.io`)，点击顶部的 **Settings** (设置) 选项卡。
2. **导航到 Pages**：在左侧导航栏中，点击 **Pages**。
3. **选择分支和文件夹**：
   - 在 "Source" 部分，选择您的**构建分支** (通常是 `main` 或 `master`)。
   - 选择**文件夹** (`/(root)` 或 `/docs`)。对于 `yourusername.github.io` 仓库，通常是 `/(root)`。
4. **重要提示**：暂时**不要**在 GitHub Pages 设置中填写 "Custom domain" (自定义域名) 部分。这一步将由 Cloudflare 处理。
5. 点击 **Save** (保存)。

GitHub Pages 会开始构建您的网站。此时，您的网站应该可以通过 `https://您的GitHub用户名.github.io` 或 `https://您的GitHub用户名.github.io/您的项目名称` 访问。

------



## 六. 将域名添加到 Cloudflare (可选)



如果您选择了使用自定义域名和 Cloudflare，请按照以下步骤操作：

1. **添加您的网站**：
   - 登录 Cloudflare 仪表盘，点击 **Add site** (添加站点) 按钮。
   - 在弹出的输入框中，精确输入您的自定义域名（例如 `yourdomain.com`，不要带 `www.` 或 `http/https://`）。
   - 点击 **Add site** (添加站点)。
2. **选择 Free 计划**：选择 "Free" 计划，然后点击 **Continue** (继续)。

------



## 七. Cloudflare 域名解析 (可选)



在 Cloudflare 中添加 DNS 记录，将您的域名指向 GitHub Pages。

1. **添加两条 CNAME 记录**：

   - **记录 1**：
     - Type: `CNAME`
     - Name: `www`
     - Content: `您的GitHub用户名.github.io`
     - Proxy status: `Proxied` (橙色云朵)
   - **记录 2**：
     - Type: `CNAME`
     - Name: `@` (代表您的裸域名，即 `yourdomain.com`)
     - Content: `您的GitHub用户名.github.io`
     - Proxy status: `Proxied` (橙色云朵)

   **重要**：这里的 Content 仍然是您的 `username.github.io`，而不是 `username.github.io/repo-name`。GitHub 会根据 CNAME 文件自动重定向。

2. **确保 Proxy status**：确保它显示为橙色云朵，这意味着您的流量将通过 Cloudflare 的 CDN 和安全服务。

3. **等待 DNS 生效**：配置完成后，等待 DNS 生效（通常需要几分钟到几小时）。

------



## 八. 完成自定义域配置 (可选)



1. **在 README 文件中填写域名**：在您的 GitHub 仓库的 `README.md` 文件中，添加一行您的域名，例如：`yourdomain.com` (不需要输入 `https://`)。GitHub Pages 会自动读取此文件来设置自定义域。
2. **在 GitHub Pages 设置中添加自定义域名**：
   - 回到您的 GitHub 仓库设置中的 **Pages** 选项卡。
   - 在 "Custom domain" 部分，直接输入您的域名（例如 `yourdomain.com`），不需要输入 `https://`。
   - 点击 **Save**。

完成这些步骤后，您的网站就可以通过自定义域名在公网进行访问了！

------



## 九. 补充及注意事项



- **Jekyll 本地文件夹路径**：Jekyll 命令行安装仓库的默认路径通常是 `C:\Users\您的用户\您的github仓库名`。一般来说不建议更改位置，因为这可能会影响环境配置。

- **Jekyll 部署逻辑**：Jekyll 的核心逻辑是将您编写的 Markdown 文件（`.md`）通过 GitHub Pages 的工作流自动转化为 HTML 文件。

- **`_posts` 文件夹**：这是博客文章的存放目录，务必遵守命名规范 (`年份-月份-日期-name.md`)，否则可能推送失败或无法正确显示。您可以在本地运行 `bundle exec jekyll serve` 来验证文章是否成功生成。

- **`_site` 文件夹**：这是 Jekyll 生成的静态网站文件目录，通常不需要手动管理，因为它是由 Jekyll 自动化部署的。

- **根目录下 `index.md`**：确保您的博客根目录下有一个 `index.md` 文件，它通常是您博客的主页。

- **图片引用**：新增 `assets` 文件夹，并在其下创建 `images` 文件夹来存放图片。引用格式如下：

  Markdown

  ```
  ![图片说明]( {{ "/assets/images/图片名称.jpg" | relative_url }} )
  ```

  **建议**：不建议使用过大的图片，这会影响页面加载速度。

- **博客层级分类**：如果希望实现类似层级分类的功能（如教程分类），您可以使用 Jekyll 的**集合 (Collections)** 功能。

  1. 在根目录下新建一个以下划线开头的文件夹，例如 `_tutorials`。

  2. 在根目录下创建对应的 Markdown 文件，例如 `tutorials.md`，并在其中编写集合的展示逻辑。

     Markdown

     ```
     ---
     layout: page # 或者其他您定义的布局
     title: "教程分类"
     permalink: /tutorials/
     ---
     
     {% assign categories = site.tutorials | map: "category" | uniq %}
     
     {% for cat in categories %}
     
       <h2>{{ cat | capitalize }}</h2>
       <ul>
         {% assign sorted = site.tutorials | where: "category", cat | sort: "lesson" %}
         {% for item in sorted %}
           <li>
             <a href="{{ item.url }}">{{ item.title }}</a>
           </li>
         {% endfor %}
       </ul>
     
     {% endfor %}
     ```

  3. 在 `_tutorials` 文件夹下添加 Markdown 文件，并按以下格式定义元数据：

     Markdown

     ```
     ---
     layout: post # 布局模式
     title: "test" # 标题
     lesson: 1 # 教程序号
     category: "Programming" # 类别
     ---
     # 这里是您的教程内容
     ```

- **自定义布局**：您可以创建 `_layouts` 文件夹来定义统一的页面布局，例如 `post.html` 或 `page.html`。

------

希望这份详细教程能帮助您顺利搭建并维护自己的 Jekyll 博客！如果您在过程中遇到任何问题，欢迎随时提问。祝您写作愉快！