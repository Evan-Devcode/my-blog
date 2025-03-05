# Hugo 搭建博客指南

Hugo 是一个快速灵活的静态网站生成器。本指南将帮助您从零开始搭建一个 Hugo 博客。

## 目录
- [安装 Hugo](#安装-hugo)
- [创建博客网站](#hugo创建博客网站步骤)
- [部署到 GitHub Pages](#部署项目到同一用户的另一个仓库的正确步骤顺序)
- [后续维护](#后续维护)

## 安装 Hugo

### Windows
待补充

### macOS
待补充

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

### 4. 安装主题
```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

### 5. 配置站点
```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```


### 6. 创建内容
```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

### 7. 本地预览
```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

### 8. 生成静态网站
```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```



## 部署项目到同一用户的另一个仓库的正确步骤顺序
### 1. 创建仓库（源码仓库和部署仓库）
### 2. 配置仓库访问权限
### 3. 创建工作流配置
### 4. 部署和验证


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







