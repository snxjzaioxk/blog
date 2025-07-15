# jekyll部署到github  page教程（详细版）



目标：搭建个人博客，在公网可以访问，本地推送文档来实现更新

准备工作：github账号(核心) 域名(可选免费域名 )  cloudflare账号（它提供了 CDN、DDoS 防护和免费 SSL）  下载ruby（jekyll所需要的环境）   git工具（本地推送到远程仓库）



## 一.创建github仓库

![gihub界面的截图]( {{ "/assets/images/image12.png" | relative_url }} )

这里默认是public，不需要更改，接下来添加一个README file（在里面添加自定义域名），仓库名必须是 `你的GitHub用户名.github.io` (例如：`octocat.github.io`)

add.gitgore里面选择jekyll，choose a license里面选择MIT License即可，点击new respository，新仓库就创建成功啦！

## 二.本地部署jekyll环境

### 1.安装Ruby和jekyll

Ruby下载地址

```
https://rubyinstaller.org/downloads/
```

安装完成后，打开命令提示符，输入

```
gem install jekyll bundler
```

检查ruby和jekyll版本

```
# 检查 Ruby 版本
ruby -v
# 检查 Gem 版本
gem -v
```



安装成功后 检测则会显示对应版本

![安装成功的截图]( {{ "/assets/images/image5.png" | relative_url }} )

等待安装成功后，执行下面命令来建立新的站点

```
jekyll new my-blog  # 将 my-blog 替换为你的博客目录名
cd my-blog
bundle install
```

### 2.本地预览博客

一定要在my-blog目录下运行命令！！

```
bundle exec jekyll serve
```

## 三.内容更新

先配置_config.yml文件，在_posts文件夹下面添加md文件即可添加文章（命名格式要规范 例如：2025-7-11-name.md，后续更新添加md文件即可

配置文件参考如下

```
title: "Aliom个人博客"#网页标题
email: 3442803364@qq.com#替换为你的邮箱地址
description: ""#描述你的网站

baseurl: ""#如果没有自定义域名 则填写你的GitHub用户名.github.io 若有自定义域名 空白即可
url: "https://bailanwa.dpdns.org"#填写自定义域名
github_username: snxjzaioxk

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



## 四.将本地仓库推送至github仓库

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

请将 `你的用户名` 替换为你的实际 GitHub 用户名

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

## 五.配置github page 

一旦代码推送到 GitHub，你需要在仓库设置中启用 GitHub Pages。

1. **进入你的 GitHub 仓库** (例如 `my-blog` 或 `yourusername.github.io`)。
2. 点击顶部的 **`Settings` (设置)** 选项卡。
3. 在左侧导航栏中，点击 **`Pages`**。
4. 在 "Source" 部分，选择你的 **构建分支** (通常是 `main` 或 `master`)，以及 **文件夹** (`/(root)` 或 `/docs`)。
5. **重要：** 暂时 **不要** 在 GitHub Pages 设置中填写 "Custom domain" (自定义域名) 部分。这一步将由 Cloudflare 处理。
6. 点击 **`Save` (保存)**。

GitHub Pages 会开始构建你的网站。在这一步，你的网站应该可以通过 `https://你的GitHub用户名.github.io` 或 `https://你的GitHub用户名.github.io/你的项目名称` 访问

## 五.将域名添加到cloudflare

添加你的网站（域名）：

- 登录 Cloudflare 仪表盘后，点击 "Add site" (添加站点) 按钮
- 在弹出的输入框中，**精确输入你的自定义域名**（例如 `yourdomain.com`，**不要**带 `www.` 或 `http/https://`）
- 点击 **"Add site" (添加站点)**

- 选择 "Free" 计划，然后点击 **"Continue" (继续)**

## 六.cloudflare域名解析

添加两条 CNAME 记录：

 `Type: CNAME`, `Name: www`, `Content: username.github.io`, `Proxy status: Proxied (橙色云朵)`

`Type: CNAME`, `Name: www`, `Content: username.github.io`, `Proxy status: Proxied (橙色云朵)` （**这里的 `Content` 仍然是你的 `username.github.io`，而不是 `username.github.io/repo-name`。GitHub 会根据 `CNAME` 文件自动重定向。**）

**`Proxy status` (橙色云朵)：** 确保它显示为橙色云朵，这意味着你的流量将通过 Cloudflare 的 CDN 和安全服务。

配置完成后，等待DNS生效即可

## 七.完成自定义域

在README文件填写域名，不需要输入https://

在github page上面添加Custom domain，直接输入域名，不需要输入https://

完成这些后，你的网站就可以通过自定义域名在公网进行访问了！

接下来是关于jekyll文件夹的说明以及补充

## 八.补充及注意事项

jekyll使用命令行安装仓库的本地文件夹默认路径是C:\Users\\用户\github仓库名，一般来说不需要更改位置，更改后可能会影响环境，不建议更改

jekyll的逻辑是上传md文件，github page工作流会自动转化为html，_posts是博客首页文件夹，需要遵守命名规范才能推送成功，（命名格式为命名格式要规范 例如：年份-月份-日期-name.md）可以运行jekyll在本地查看是否成功

_size文件夹是自动化部署的文件夹，不需要管

根目录下一定要有index.md

增添图片的话，新增assets文件夹，在这个文件夹下设images文件夹，添加图片，若要引用，格式为

```
![图片说明]( {{ "/assets/images/图片名称" | relative_url }} )
```

不建议太大的图片，加载会比较慢

想要和我这个博客一样，有层级分类的话，在jekyll中使用集合，也就是根目录下新建_tutorials文件夹，也需要在根目录下添加tutorials.md文件

tutorials.md文件示例

```

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

在_tutorials文件夹下添加md文件,格式如下

```
layout: post#布局模式
title: "test"#标题
lesson: 1
category: #类别
```

也可创建_layout文件夹，设置统一格式

教程到这里也就结束了，感谢观看，希望对你建立自己的博客有所帮助吧！