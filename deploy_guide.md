# 部署指南 — AI 校园地图生成器

> 从本地文件到公网可访问的 URL，最快 2 分钟完成。

---

## 方案一：Vercel（推荐，最快）

### 前置条件
- 有 GitHub 账号（参考 C5A 注册流程）
- 项目已推送到 GitHub

### 步骤

1. **访问 vercel.com**，用 GitHub 账号登录
2. 点击右上角 **Add New...** → **Project**
3. 在列表中找到你的 repo（ai-campus-map-generator），点击 **Import**
4. 配置页面保持默认（Framework Preset 选 Other，Build Command 留空，Output Directory 填 `.`）
5. 点击 **Deploy**
6. 等待 1-2 分钟，部署完成后自动跳转到项目页面
7. 点击 **Visit** 按钮，获得你的公网 URL（格式：`https://ai-campus-map-generator-xxx.vercel.app`）

### 后续更新
每次 push 到 GitHub，Vercel 会自动重新部署。

---

## 方案二：Netlify（拖拽部署，无需 GitHub）

### 步骤

1. **访问 app.netlify.com**，注册/登录
2. 进入 **Sites** 页面
3. 将整个 `ai-campus-map-generator` 文件夹**拖拽**到页面中的虚线区域
4. 等待上传和部署完成（通常 30 秒内）
5. 获得公网 URL（格式：`https://xxx.netlify.app`）

### 自定义域名
在 Site settings → Domain management 中可以修改子域名。

---

## 方案三：GitHub Pages（完全免费，与 C5 联动）

### 步骤

1. 确保项目已推送到 GitHub
2. 进入 repo 的 **Settings** → **Pages**
3. **Source** 选择 `Deploy from a branch`
4. **Branch** 选择 `main`，文件夹选择 `/ (root)`
5. 点击 **Save**
6. 等待 1-3 分钟，页面顶部会显示 URL（格式：`https://你的用户名.github.io/ai-campus-map-generator/`）

---

## 方案四：本地预览（不上线）

如果只是想在本地查看效果：

```bash
# Python
python3 -m http.server 8080

# Node.js
npx serve .

# 或直接双击 index.html 用浏览器打开
```

然后访问 http://localhost:8080

---

## 部署后检查清单

- [ ] URL 可以公开访问（不需要登录你的开发环境）
- [ ] 30 秒内能看懂这个 App 是干什么的
- [ ] Demo 模式点击生成后地图正常显示
- [ ] 地图可以缩放、点击标记显示弹窗
- [ ] 地点清单正常显示
- [ ] 手机浏览器也能正常使用（响应式布局）
- [ ] 页面加载时间 < 5 秒
- [ ] 没有 API Key 硬编码在代码里（AI 模式由用户输入）

---

## 常见问题

### Q：部署后地图不显示？
A：检查网络连接，OpenStreetMap 底图需要联网加载。某些公司网络可能屏蔽了 tile 服务器。

### Q：AI 模式调用失败？
A：检查 API Key 是否正确、API 地址是否可访问、模型名称是否正确。可以在浏览器开发者工具（F12）的 Network 标签中查看具体错误。

### Q：怎么绑定自己的域名？
A：Vercel 和 Netlify 都支持自定义域名，在项目设置中添加即可。GitHub Pages 需要在 repo 设置中配置 CNAME。

### Q：Vercel 免费额度够用吗？
A：Vercel Hobby 计划每月 100GB 带宽，对于课程项目完全足够。
