# 🌐 个人网站
<div align="center">

<img src="website\public\favicon.ico" alt="LiteIsle Logo" width="60" height="60">

</div>

## 📖 项目简介

这是一个使用 Vue 3 + TypeScript + Vite 构建的个人项目展示站点，包含多个项目卡片与动效展示。

## ✨ 功能特性

- 🎞️ 项目卡片滚动进入视口的渐显与位移动画
- 🌌 图片容器 3D 视角与柔和氛围光，主图 + 覆盖图卡片化叠层
- 🔗 链接图标按钮：左侧“外链”图标跳转 Demo，右侧 GitHub 图标
- 📱 响应式布局，移动端尺寸与叠层位置优化

## 🛠 技术栈

- Vue 3 + TypeScript
- Vite
- Tailwind CSS（已配置，可按需使用）
- PostCSS / Autoprefixer

## 💻 本地开发

```bash
cd portfolio-website
npm ci
npm run dev
```

打开浏览器访问开发服务器提示地址（通常为 `http://localhost:5173/`）。

## 📦 构建与本地预览

```bash
cd portfolio-website
npm run build
npm run preview
```

产物输出目录：`portfolio-website/dist`

## 🚀 部署到 GitHub Pages

### 只托管静态文件（双仓库）

1. 在本地构建产物：`cd website && npm ci && npm run build`
2. 将 `portfolio-website/dist` 中的所有文件复制到 `{user_name}.github.io` 仓库根目录并推送
3. 启用 Pages，访问 `https://{user_name}.github.io/`

## 目录结构

```text
portfolio-website/
  package.json
  package-lock.json
  vite.config.ts
  tailwind.config.js
  postcss.config.js
  tsconfig*.json
  public/
  src/
    main.ts
    App.vue
    views/
      HomeView.vue
      ProjectsView.vue
      AboutView.vue
```

## 📜 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情


