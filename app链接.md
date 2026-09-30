# C6 Web App 链接与部署说明

> 项目名称：AI 校园地图生成器 (AI Campus Map Generator)
> 一句话说明：输入地点名称，AI 自动生成带分类标记的交互式地图 — 零代码，秒级出图

---

## 部署后的 URL

```
https://fu-yue-ccc.github.io/c6-ai-campus-map/
```

> ⬆️ 上方为 GitHub Pages 正式上线地址（源码仓库：https://github.com/Fu-yue-ccc/c6-ai-campus-map ）。如需换成 Vercel / Netlify 自有域名，可按下方步骤再部署一次并替换本行。

---

## 群内分享话术

> 这是我的 C6 Web App：https://fu-yue-ccc.github.io/c6-ai-campus-map/ — 输入任意地点名称就能生成交互式地图，Demo 模式免 API Key 直接体验，大家试试看，欢迎反馈！

---

## 部署步骤（5 分钟上线）

### 方法一：Vercel（推荐）

1. 将 `C6_WebApp/` 文件夹推送到 GitHub（参考 C5 流程）
2. 访问 [vercel.com](https://vercel.com)，用 GitHub 登录
3. 点击 **Add New...** → **Project**
4. 选择你的 repo → **Import**
5. 配置保持默认 → 点击 **Deploy**
6. 2 分钟后获得公网 URL

### 方法二：Netlify（拖拽部署，无需 GitHub）

1. 访问 [app.netlify.com](https://app.netlify.com)
2. 将整个 `C6_WebApp/` 文件夹拖拽到部署区域
3. 30 秒后获得 URL

### 方法三：GitHub Pages

1. 推送到 GitHub
2. Settings → Pages → Source 选 main branch
3. 几分钟后获得 `https://用户名.github.io/项目名/`

---

## 本地预览

```bash
cd C6_WebApp
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

或直接双击 `index.html` 用浏览器打开。

---

## 功能清单

- ✅ Demo 模式：内置 SIAS 大学 12 个真实地点，免 API Key
- ✅ AI 模式：支持 OpenAI / DeepSeek / 智谱等兼容 API
- ✅ 交互式地图：Leaflet.js 渲染，可缩放、点击标记
- ✅ 分类着色：12 种地点分类，自动图例
- ✅ 地点清单：点击可定位到地图标记
- ✅ 导出 JSON：一键下载地点数据
- ✅ 响应式设计：手机/平板/电脑均可使用
- ✅ 加载时间 < 5 秒（纯静态，CDN 加速）

---

## AI 集成层次

**进阶层次（多步骤 workflow）**：用户输入 → AI 生成结构化 JSON → 自动验证坐标 → 渲染交互式地图 → 支持导出。

> 不是"用 AI 写了代码"，而是产品本身调用 AI 作为核心功能。
