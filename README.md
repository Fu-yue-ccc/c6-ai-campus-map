# AI 校园地图生成器 (AI Campus Map Generator)

> 输入地点名称，AI 自动生成带分类标记的交互式地图。零代码，秒级出图。

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/你的用户名/ai-campus-map-generator)

---

## 这是什么

一个基于纯前端的 AI 驱动地图生成器：
- **输入**：地点名称 + 生成数量
- **AI 处理**：调用 OpenAI 兼容 API 生成结构化地点 JSON
- **输出**：Leaflet.js 交互式地图（可缩放、点击标记、分类着色、图例）
- **Demo 模式**：内置 SIAS 大学 12 个真实地点数据，无需 API Key 即可体验

---

## 快速开始

### 本地运行

```bash
# 克隆或下载本项目
cd ai-campus-map-generator

# 直接用浏览器打开 index.html 即可
# 或启动本地服务器：
python3 -m http.server 8080
# 然后访问 http://localhost:8080
```

### Demo 模式（无需 API Key）

1. 打开页面，默认选择 "Demo 模式"
2. 地点名称填 "郑州西亚斯学院"，数量填 10
3. 点击 "生成地图"
4. 秒级生成包含 12 个真实地点的交互式地图

### AI 模式（需要 API Key）

1. 切换到 "AI 模式"
2. 填入 API 地址（默认 OpenAI，可改 DeepSeek、智谱等兼容接口）
3. 填入 API Key 和模型名称（如 gpt-4o-mini、deepseek-chat）
4. 输入任意地点名称，点击生成

> 🔒 API Key 仅在浏览器本地使用，不会上传到任何服务器。

---

## 技术栈

| 层次 | 技术 | 说明 |
|------|------|------|
| UI 框架 | Tailwind CSS (CDN) | 原子化 CSS，零构建 |
| 地图引擎 | Leaflet.js 1.9.4 | 轻量级交互式地图库 |
| 地图数据 | OpenStreetMap | 免费开源底图 |
| AI 接口 | OpenAI 兼容 API | 支持 OpenAI / DeepSeek / 智谱 / 本地 Ollama |
| 语言 | 原生 JavaScript | 零框架依赖，单文件部署 |

---

## AI 集成层次

本项目达到 **进阶层次**（多步骤 workflow）：

1. 用户输入地点名称和数量
2. System Prompt 强制 AI 输出 valid JSON（结构化输出）
3. 前端自动验证坐标范围和字段完整性
4. 验证通过后渲染为交互式地图
5. 支持导出 JSON 数据

---

## 部署到 Vercel（推荐）

### 方法一：网页部署（最简单）

1. 将本项目推送到 GitHub（参考 C5 流程）
2. 访问 [vercel.com](https://vercel.com)，用 GitHub 登录
3. 点击 "Add New" → "Project"
4. 选择你的 repo，点击 "Deploy"
5. 2 分钟后获得 `https://xxx.vercel.app` 链接

### 方法二：CLI 部署

```bash
npm install -g vercel
cd ai-campus-map-generator
vercel
# 按提示操作，完成后获得部署链接
vercel --prod  # 部署到生产环境
```

### 方法三：Netlify

1. 访问 [app.netlify.com](https://app.netlify.com)
2. 拖拽整个项目文件夹到部署区域
3. 立即获得 `https://xxx.netlify.app` 链接

### 方法四：GitHub Pages

1. 推送到 GitHub
2. Settings → Pages → Source 选 main branch
3. 几分钟后获得 `https://你的用户名.github.io/ai-campus-map-generator/`

---

## 项目结构

```
ai-campus-map-generator/
├── index.html          # 主应用（单文件，包含所有 HTML/CSS/JS）
├── README.md           # 本文件
├── deploy_guide.md     # 详细部署指南
└── ATTRIBUTION.md      # 借鉴来源说明
```

---

## 自定义

### 修改 Demo 数据

编辑 `index.html` 中的 `DEMO_DATA` 数组，替换为你想要的地点数据。

### 添加新的地点分类颜色

编辑 `CATEGORY_COLORS` 对象，添加新的分类和对应颜色。

### 修改 AI System Prompt

编辑 `callAI()` 函数中的 `systemPrompt`，可以添加更严格的坐标要求、描述长度限制等。

---

## 与 C4/C5 的联动

- **C4D**：本项目基于 C4D 的本地大模型地图 Agent，将 Python 脚本升级为 Web App
- **C5**：源码可直接推送到 C5 创建的 GitHub repo，实现一石二鸟

---

## License

MIT
