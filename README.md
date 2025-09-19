# 圆方魔方俱乐部宣传网站

这是圆方魔方俱乐部的官方宣传网站，展示了俱乐部的特色、课程、师资力量和学员评价等内容。

## 项目介绍

- 采用现代化的React+TypeScript+Tailwind CSS技术栈开发
- 响应式设计，支持PC端和移动端访问
- 包含主题切换功能，支持亮色/暗色模式
- 丰富的动画效果，提升用户体验

## 如何在本地运行

1. 确保您的电脑已安装Node.js和pnpm
2. 克隆或下载此项目
3. 在项目根目录运行以下命令：

```bash
# 安装依赖
pnpm install

# 启动开发服务器
pnpm dev
```

4. 打开浏览器，访问 http://localhost:3000 查看效果

## 如何部署到免费网页空间

以下是将网站部署到几个常见的免费网页空间的详细步骤：

### 方法一：使用Vercel部署（推荐）

Vercel是一个免费的托管平台，特别适合部署React等前端项目。

**步骤1：准备工作**
1. 注册一个GitHub账号（如果没有的话）
2. 将项目代码上传到GitHub仓库
3. 注册一个Vercel账号（可以使用GitHub账号直接登录）

**步骤2：部署到Vercel**
1. 登录Vercel，点击"New Project"按钮
2. 选择您刚刚创建的GitHub仓库
3. 点击"Import"按钮
4. 在配置页面，保持默认设置不变
5. 点击"Deploy"按钮开始部署
6. 等待部署完成，Vercel会为您生成一个域名，您可以通过这个域名访问您的网站

### 方法二：使用Netlify部署

Netlify也是一个常用的免费托管平台，部署过程简单直观。

**步骤1：准备工作**
1. 注册一个GitHub账号（如果没有的话）
2. 将项目代码上传到GitHub仓库
3. 注册一个Netlify账号

**步骤2：部署到Netlify**
1. 登录Netlify，点击"New site from Git"按钮
2. 选择"GitHub"作为Git提供商
3. 授权Netlify访问您的GitHub仓库
4. 选择您的项目仓库
5. 在部署配置页面：
   - 构建命令：`pnpm build`
   - 发布目录：`dist`
6. 点击"Deploy site"按钮开始部署
7. 部署完成后，Netlify会为您的网站分配一个临时域名

### 方法三：使用GitHub Pages部署

GitHub Pages是GitHub提供的免费静态网站托管服务。

**步骤1：准备工作**
1. 注册一个GitHub账号（如果没有的话）
2. 将项目代码上传到GitHub仓库

**步骤2：配置项目**
1. 在项目根目录创建一个`.github/workflows/deploy.yml`文件
2. 将以下内容复制到该文件中：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: "20"
      - name: Install dependencies
        run: npm install -g pnpm && pnpm install
      - name: Build
        run: pnpm build
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: "./dist"
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

**步骤3：启用GitHub Pages**
1. 进入您的GitHub仓库页面
2. 点击"Settings"选项卡
3. 在左侧导航栏中选择"Pages"
4. 在"Build and deployment"部分，选择"Deploy from a branch"
5. 在"Branch"下拉菜单中选择`gh-pages`和`/(root)`
6. 点击"Save"按钮
7. 等待GitHub Actions完成构建和部署过程
8. 部署完成后，您可以通过`https://[您的GitHub用户名].github.io/[仓库名称]`访问您的网站

## 自定义域名（可选）

如果您有自己的域名，可以将其绑定到已部署的网站上：

1. 在您的域名注册商处，添加CNAME记录指向托管平台提供的域名
2. 在托管平台（Vercel/Netlify/GitHub Pages）的设置中添加自定义域名
3. 按照平台的指示完成域名验证和SSL证书配置

## 常见问题及解决方案

1. **部署失败，提示缺少依赖**
   - 确保您的`package.json`文件中包含了所有必要的依赖
   - 尝试在本地运行`pnpm build`命令，确保本地构建成功

2. **页面加载后样式错乱**
   - 检查Tailwind CSS的配置是否正确
   - 确保`index.html`文件中的路径引用正确

3. **网站图片无法显示**
   - 检查图片路径是否正确
   - 确保图片文件已包含在构建产物中

如果您在部署过程中遇到其他问题，可以查看托管平台提供的错误日志，或者在网上搜索相关解决方案。