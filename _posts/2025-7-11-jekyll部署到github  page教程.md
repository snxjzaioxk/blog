# jekyll部署到github  page教程



## 创建github page仓库

![这是一个截图，用来解释说明的]( {{ "/assets/images/image12.png" | relative_url }} )

默认是public，这个不需要更改，接下来添加一个README file（在里面添加自定义域名），

add.gitgore里面选择jekyll，choose a license里面选择MIT License即可，点击new respository，新仓库就创建成功啦！

## 配置jekyll

### 本地搭建jekyll并推送到github(灵活度高)

### 1.安装Ruby和jekyll

Ruby下载地址

```
https://rubyinstaller.org/downloads/
```

安装完成后，打开命令提示符，输入

```
gem install jekyll bundler
```

等待安装成功后，执行下面命令来建立新的站点

```
jekyll new my-blog  # 将 my-blog 替换为你的博客目录名
cd my-blog
bundle install
```

### 2.本地预览博客

在my-blog目录下运行

```
bundle exec jekyll serve
```

### 3.内容更新

先配置_config.yml文件，在_posts文件夹下面添加md文件即可添加文章（命名格式要规范 例如：2025-7-11-name.md，后续更新添加md文件即可

#### 4.将本地仓库推送至github仓库

准备工作：安装git工具

下载地址

```
https://git-scm.com/downloads
```

**初始化 Git 仓库**： 如果你的 `my-blog` 目录还没有 Git 仓库，需要先初始化：

```
git init
```

**关联远程仓库**： 将本地仓库与你在第一步创建的 `你的用户名.github.io` 远程仓库关联：

```
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
```

请将 `你的用户名` 替换为你的实际 GitHub 用户名。

**添加所有文件并提交**：

```
git add .
git commit -m "Initial Jekyll blog setup"
```

**推送到 GitHub**：

```
git branch -M main # 将主分支重命名为 main (如果不是)
git push origin main
```

如果推送失败，运行下面命令行

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

它们的作用是移除 Git 的全局 HTTP 和 HTTPS 代理配置，让 Git 直接尝试连接远程服务器



有时候取消代理设置仍然会出现报错，这时可以通过设置系统代理来解决。具体步骤如下：

在代理服务器中，将端口设置为7890，在终端输入以下命令，设置 Git 使用本地代理

```text
git config --global http.proxy http://127.0.0.1:7890
```

设置完成后，可以通过以下命令检验是否设置成功：

```text
git config --global -l
```