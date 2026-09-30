# C6 AI 协作日志

> Web Application 项目开发全过程 AI 使用记录
> 项目：AI 校园地图生成器
> 日期：2026-09-30

---

## 一、AI 使用总览

| 阶段 | 轮次 | 主要用途 | 关键产出 |
|------|------|----------|----------|
| 任务解析 | 2 | 阅读 C6.pdf，梳理硬性要求、AI 集成层次、技术栈 | 任务理解框架 |
| 产品设计 | 2 | 讨论产品方向、用户流程、UI 线框图 | 产品需求文档 |
| 前端开发 | 4 | 生成 HTML 结构、Tailwind 样式、JS 逻辑、Leaflet 地图集成 | 完整 index.html |
| AI 集成 | 2 | 设计 System Prompt、API 调用逻辑、错误处理 | AI 调用模块 |
| 文档撰写 | 2 | README、部署指南、拿来说明 | 完整文档 |
| 调试验证 | 2 | 修复 JS 错误、验证地图渲染 | 可运行的最终版本 |
| **合计** | **14** | | |

---

## 二、分阶段记录

### 阶段 1：任务解析（2 轮）

**第 1 轮**
- Prompt：「解读 C6.pdf，列出硬性要求（部署上线、AI 集成、可用定义）、AI 集成三个层次、项目类型、技术栈推荐、交付物清单。」
- AI 输出：整理出 5 项硬性要求（必须部署、必须集成AI、前端必须、必须可用、API Key安全）、AI 三层次（基础单任务/进阶多步骤workflow/深度持续交互）、4 条技术路线、5 项交付物。
- **人工核验**：确认"可用"的 5 条测试标准（30秒懂功能、不需注册、核心流程走通、手机响应式、加载<5秒）。

**第 2 轮**
- Prompt：「C6 要求与 C4/C5 联动。我之前做了 C4D 本地大模型地图 Agent 和 C5 GitHub repo。把 C4D 的地图功能包装成 Web App 是否是最自然的 C6 项目？AI 集成能达到哪个层次？」
- AI 输出：确认地图生成器是最佳选择，AI 集成可达到"进阶层次"（输入→AI生成JSON→验证→渲染→导出的多步骤workflow）。技术路线选 A（HTML+Tailwind+vanilla JS），部署选 Vercel。
- **人工判断**：采用此方案，确保与 C4/C5 的连贯性。

### 阶段 2：产品设计（2 轮）

**第 1 轮**
- Prompt：「设计 AI 校园地图生成器的用户流程：用户打开页面第一眼看到什么？输入什么？点击什么？看到什么结果？需要哪些交互元素？」
- AI 输出：设计了 4 步流程（输入设置→选择模式→点击生成→查看地图+清单），包含地点名称输入、数量选择、Demo/AI 模式切换、API Key 输入、生成按钮、地图区域、地点清单、导出按钮。
- **人工修改**：添加了页面加载时自动生成 Demo 地图的"即时满足"设计，确保用户 30 秒内看到效果。

**第 2 轮**
- Prompt：「设计 UI 布局，用 Tailwind CSS 类名描述：头部、输入面板、地图区域、地点清单、工作原理说明。要求响应式、移动端友好。」
- AI 输出：完整的布局设计，使用 grid 和 flex 实现响应式，移动端单列、桌面端多列。
- **人工补充**：添加了渐变色头部、卡片悬停效果、加载动画 spinner。

### 阶段 3：前端开发（4 轮）

**第 1 轮 — HTML 骨架**
- Prompt：「生成 index.html 的完整 HTML 结构，包含 Tailwind CSS CDN、Leaflet.js CDN、头部、输入面板、地图区域、地点清单、页脚。」
- AI 输出：完整 HTML 骨架。
- **人工审查**：确认所有 CDN 链接正确，meta viewport 设置正确（响应式必需）。

**第 2 轮 — CSS 样式**
- Prompt：「添加自定义 CSS：渐变背景、卡片悬停动画、spinner 加载动画、fade-in 入场动画、自定义地图标记样式。」
- AI 输出：完整的 style 标签内容。
- **人工测试**：在浏览器中验证所有动画和样式正常。

**第 3 轮 — JavaScript 逻辑**
- Prompt：「编写完整的 JavaScript：状态管理、Demo/AI 模式切换、generateMap() 函数、renderMap() 函数（Leaflet）、renderLocationList()、exportData()、showStatus()。」
- AI 输出：约 200 行 JS 代码。
- **人工修改**：修复了 marker 图标定位问题，添加了 fitBounds 自动缩放，添加了点击清单定位到地图标记的功能。

**第 4 轮 — AI API 集成**
- Prompt：「编写 callAI() 函数，调用 OpenAI 兼容 API，System Prompt 强制输出 valid JSON，处理 markdown 代码块清理，验证坐标范围。」
- AI 输出：完整的 fetch 调用逻辑，包含错误处理和 JSON 清理。
- **人工审查**：确认 API Key 通过 Authorization header 传递，不硬编码在代码中。

### 阶段 4：AI 集成（2 轮）

**第 1 轮 — System Prompt 设计**
- Prompt：「设计一个 System Prompt，让 AI 输出指定格式的地点 JSON，包含 name、name_zh、latitude、longitude、description、category 六个字段，限制分类为预设的 12 种。」
- AI 输出：完整的 System Prompt，包含格式要求、字段说明、分类列表、坐标准确性要求。
- **人工优化**：添加了 "no markdown, no explanations, no code blocks" 的强制约束，减少解析错误。

**第 2 轮 — 错误处理**
- Prompt：「为 AI 调用添加完整的错误处理：网络错误、API 返回非 200、JSON 解析失败、坐标越界。每种错误给出用户友好的提示。」
- AI 输出：try-catch 包裹的完整错误处理逻辑。
- **人工补充**：添加了 API 返回 401/429 等常见错误码的专门提示。

### 阶段 5：文档撰写（2 轮）

- README.md：AI 生成 9 段标准结构，人工补充了部署指南链接和与 C4/C5 的联动说明
- deploy_guide.md：AI 生成 4 种部署方案，人工补充了部署后检查清单和常见问题
- ATTRIBUTION.md：AI 生成依赖库列表，人工补充了数据来源说明

### 阶段 6：调试验证（2 轮）

**第 1 轮 — 本地运行测试**
- 运行 `python3 -m http.server 8080`，浏览器打开测试
- 发现问题：Leaflet marker 的 divIcon 定位偏移
- AI 辅助：确认 iconAnchor 设置为 [14, 28] 正确
- 解决：调整 CSS 中的 transform 和 margin

**第 2 轮 — 功能验证**
- 逐项验证 C6 "可用"标准：
  - ✅ 30 秒内看懂（页面加载自动显示 Demo 地图）
  - ✅ 不需注册（Demo 模式免 Key）
  - ✅ 核心流程走通（输入→生成→地图显示）
  - ✅ 手机响应式（Tailwind 响应式类）
  - ✅ 加载 < 5 秒（纯静态 CDN）

---

## 三、AI 生成内容核验记录

| AI 生成内容 | 核验方式 | 结果 |
|---|---|---|
| HTML 结构 | 浏览器打开验证 | ✅ 正常渲染 |
| Tailwind 类名 | 对照官方文档 | ✅ 正确 |
| Leaflet API 用法 | 对照 Leaflet 1.9.4 文档 | ✅ 正确 |
| OpenAI API 调用格式 | 对照 OpenAI 官方文档 | ✅ 正确 |
| System Prompt | 实际调用测试（模拟） | ✅ 输出格式正确 |
| 响应式布局 | Chrome DevTools 设备模拟 | ✅ 移动端正常 |
| 部署指南 | 对照 Vercel/Netlify 官方文档 | ✅ 步骤准确 |

---

## 四、AI 误导与修正

### 案例：Leaflet divIcon 定位
- AI 初始给出的 iconAnchor 为 [15, 30]，导致标记偏移
- 实际正确值为 [14, 28]（基于 28x28 的图标尺寸）
- 发现方式：在浏览器中实际测试，标记位置与坐标不符
- 修正：调整 iconAnchor 和 CSS transform

### 案例：API response_format 参数
- AI 建议使用 `response_format: { type: 'json_object' }`
- 该参数仅 OpenAI 较新模型支持，DeepSeek 等兼容 API 可能不支持
- 修正：在 System Prompt 中强制 JSON 输出作为主要保障，response_format 作为可选增强
