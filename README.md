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
  <summary>点击展开代码</summary>
     yaml
  baseurl: https://evan-devcode.github.io/my-blog/  
  languageCode: zh-cn  
  title: Evan's Blog  
  theme: hugo-theme-stack  
  copyright: Example Person  
</details> 




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







