# Hugo 搭建博客指南

Hugo 是一个快速灵活的静态网站生成器。本指南将帮助您从零开始搭建一个 Hugo 博客。

## 目录
- [安装 Hugo](#安装-hugo)
- [创建博客网站](#hugo创建博客网站步骤)
- [部署到 GitHub Pages](#部署项目到同一用户的另一个仓库的正确步骤顺序)
- [后续维护](#后续维护)

## 安装 Hugo

### Windows
请参考 [Hugo 官方文档](https://gohugo.io/installation/windows/) 进行安装。

### macOS
```sh
brew install hugo
```

### Linux
```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.145.0/hugo_extended_0.145.0_linux-amd64.debwget
sudo dpkg -i hugo_extended_0.145.0_linux-amd64.deb
```

## hugo创建博客网站步骤
### 1. 创建新站点
```bash
hugo new site my-blog
cd my-blog
```

### 2. 目录结构
```bash
my-site/                     # Hugo 站点的根目录
├── archetypes/              # 内容模板文件
├── assets/                  # Hugo Pipes 处理的静态资源
├── config/                  # 配置文件目录
├── content/                 # 内容文件目录
├── data/                    # 数据文件目录
├── layouts/                 # 模板文件目录
├── static/                  # 静态文件目录
├── themes/                  # 主题目录
└── public/                  # 生成的静态网站文件
```

### 3. 初始化仓库
```bash
git init
```

### 4. 安装配置主题
```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

#### Stack 主题目录结构
```
hugo-theme-stack/
├── assets/                  # 静态资源文件
├── i18n/                    # 国际化语言文件
├── layouts/                 # 模板文件
├── archetypes/             # 内容模板
├── static/                 # 静态文件
└── exampleSite/           # 示例站点
```

#### 
复制示例内容（可选）
```
cp -r themes/hugo-theme-stack/exampleSite/* .
```

### 5. 配置站点
修改 hugo.toml 或 hugo.yaml 文件，更新 baseURL 变量。

<details>
  <summary>点击展开 Hugo 配置文件</summary>

  ```yaml
  # Hugo 站点的基本配置信息 
  baseurl: https://evan-devcode.github.io/my-blog/  # 站点的基础 URL，部署到 GitHub Pages 时需填写完整 URL
  languageCode: zh-cn  # 站点的默认语言（中文）
  title: Evan's Blog  # 网站标题
  theme: hugo-theme-stack  # 使用的 Hugo 主题
  copyright: Example Person  # 版权信息

  # 主题的国际化支持
  DefaultContentLanguage: zh-cn  # 站点默认语言（可选值见注释）
  hasCJKLanguage: false  # 若站点使用 CJK 语言（中文、日文、韩文），设置为 true 以优化字数统计等功能

  languages:
      zh-cn:
          languageName: 中文  # 语言显示名称
          title: Evan's Blog  # 站点标题
          weight: 2  # 语言权重，数字越小优先级越高
          params:
              sidebar:
                  subtitle:  # 侧边栏副标题

  # 第三方服务配置
  services:
      disqus:
          shortname: "hugo-theme-stack"  # Disqus 评论系统的短名称
      googleAnalytics:
          id:  # Google Analytics 跟踪 ID

  # 文章分页配置
  pagination:
      pagerSize: 3  # 分页时，每页显示的文章数量

  # 文章链接的自定义格式
  permalinks:
      post: /p/:slug/  # 文章的永久链接格式
      page: /:slug/  # 页面（非文章）的永久链接格式

  # 站点参数配置
  params:
      mainSections:
          - post  # 主要内容的分类
      featuredImageField: image  # 文章特色图片字段
      rssFullContent: true  # RSS 订阅输出全文
      favicon:  # 站点 favicon

      footer:
          since: 2020  # 站点创建年份
          customText:  # 页脚自定义文本

      dateFormat:
          published: Jan 02, 2006  # 文章发布时间格式
          lastUpdated: Jan 02, 2006 15:04 MST  # 文章更新时间格式

      sidebar:
          emoji: 🍥  # 侧边栏图标
          subtitle: Lorem ipsum dolor sit amet, consectetur adipiscing elit.  # 侧边栏副标题
          avatar:
              enabled: true  # 是否显示头像
              local: true  # 头像是否本地存储
              src: img/avatar.png  # 头像图片路径

      article:
          math: false  # 是否启用数学公式支持
          toc: true  # 是否显示目录
          readingTime: true  # 是否显示阅读时间
          license:
              enabled: true  # 是否启用文章版权声明
              default: Licensed under CC BY-NC-SA 4.0  # 文章默认许可证

      comments:
          enabled: true  # 是否启用评论
          provider: disqus  # 默认使用 Disqus 评论系统

  # 小工具配置
  widgets:
      homepage:
          - type: search  # 搜索框
          - type: archives  # 归档
            params:
                limit: 5  # 显示最近 5 篇文章
          - type: categories  # 分类
            params:
                limit: 10
          - type: tag-cloud  # 标签云
            params:
                limit: 10
      page:
          - type: toc  # 页面目录（Table of Contents）

  # Open Graph 配置（社交媒体分享）
  opengraph:
      twitter:
          site:  # Twitter 用户名
          card: summary_large_image  # 分享卡片类型

  # 颜色主题配置
  colorScheme:
      toggle: true  # 是否显示深浅色主题切换按钮
      default: auto  # 默认主题，可选值：auto, light, dark

  # 图片处理配置
  imageProcessing:
      cover:
          enabled: true
      content:
          enabled: true
</details> ```







# 小工具配置
widgets:
    homepage:
        - type: search  # 搜索框
        - type: archives  # 归档
          params:
              limit: 5  # 显示最近 5 篇文章
        - type: categories  # 分类
          params:
              limit: 10
        - type: tag-cloud  # 标签云
          params:
              limit: 10
    page:
        - type: toc  # 页面目录（Table of Contents）

# Open Graph 配置（社交媒体分享）
opengraph:
    twitter:
        site:  # Twitter 用户名
        card: summary_large_image  # 分享卡片类型

# 默认 Open Graph 图片
defaultImage:
    opengraph:
        enabled: false
        local: false
        src:

# 颜色主题配置
colorScheme:
    toggle: true  # 是否显示深浅色主题切换按钮
    default: auto  # 默认主题，可选值：auto, light, dark

# 图片处理配置
imageProcessing:
    cover:
        enabled: true
    content:
        enabled: true

# 自定义菜单
menu:
    main: []  # 主要菜单

    social:
        - identifier: github
          name: GitHub
          url: https://github.com/CaiJimmy/hugo-theme-stack
          params:
              icon: brand-github

        - identifier: twitter
          name: Twitter
          url: https://twitter.com
          params:
              icon: brand-twitter

# 相关文章推荐
related:
    includeNewer: true  # 是否包括较新的文章
    threshold: 60  # 相关性阈值
    toLower: false
    indices:
        - name: tags
          weight: 100  # 标签权重
        - name: categories
          weight: 200  # 分类权重

# Markdown 解析器配置
markup:
    goldmark:
        extensions:
            passthrough:
                enable: true
                delimiters:
                    block:
                        - - \[
                          - \]
                        - - $$
                          - $$
                    inline:
                        - - \(
                          - \)
        renderer:
            unsafe: true  # 允许 Markdown 中包含 HTML 代码
    tableOfContents:
        endLevel: 4  # 目录最大层级
        ordered: true  # 目录是否为有序列表
        startLevel: 2  # 目录起始层级
    highlight:
        noClasses: false
        codeFences: true  # 代码块是否高亮
        guessSyntax: true  # 自动识别代码语言
        lineNoStart: 1  # 代码行号起始值
        lineNos: true  # 是否显示行号
        lineNumbersInTable: true  # 行号是否使用表格格式
        tabWidth: 4  # 代码缩进宽度
```






### 6. 创建内容
```bash
hugo new post/my-first-post/index.md
```

### 7. 本地预览
```bash
hugo server -D
```

### 8. 生成静态网站
```bash
hugo
```



## 部署项目到同一用户的另一个仓库的正确步骤顺序
> ### 1. 创建仓库（源码仓库和部署仓库）
> ### 2. 配置仓库访问权限
> ### 3. 创建工作流配置
> ### 4. 部署和验证

### GitHub Actions 部署配置
#### **Token 认证方式**
1. 访问 GitHub [Developer Settings](https://github.com/settings/tokens) 生成 **Personal Access Token (PAT)**。
2. 选择 `repo` 权限。
3. 在 **源代码仓库** 的 `Settings -> Secrets and variables -> Actions` 添加 `PERSONAL_TOKEN`。

#### **SSH 认证方式**
```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f gh-pages-deploy
```
- 将 `gh-pages-deploy.pub` 添加到 **目标仓库** 的 `Deploy Keys`。
- 将 `gh-pages-deploy` 私钥添加到 **源代码仓库** 的 `Actions Secrets`。

### 1. 配置 GitHub Actions
创建 `.github/workflows/deploy.yml` 文件，内容如下：
```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify --baseURL https://your-username.github.io/

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          personal_token: ${{ secrets.PERSONAL_TOKEN }}
          external_repository: your-username/your-username.github.io
          publish_branch: main
          publish_dir: ./public
```

### 2. 推送到远程仓库
```sh
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/your-username/blog-source.git
git push -u origin main
```

### 3. 启用 GitHub Pages
在 **目标仓库** (`your-username.github.io`) 的 `Settings -> Pages` 中，选择 `main` 分支并保存。

### 4. 验证部署
访问 `https://your-username.github.io/` 查看博客。

## 后续维护
### 添加新文章
```
hugo new post/新文章标题.md
```

### 更新网站
```
git add .
git commit -m "添加新文章"
git push
```







