# 本草知体 APP 完整安装与部署指南

## 一、本地快速体验（推荐先做）

### 方法 1：直接打开（最简单）
1. 下载仓库中的 `index.html`
2. 用手机或电脑浏览器直接打开该文件
3. 建议用手机 Chrome / Safari，并「添加到主屏幕」获得类原生体验

### 方法 2：本地 HTTP 服务
```bash
# 进入项目目录
cd bencao-zhiti-app

# 启动服务
python3 -m http.server 8080
# 或
npx serve .

# 浏览器访问 http://localhost:8080
```

## 二、GitHub 仓库安装

```bash
git clone https://github.com/sandy01384007/bencao-zhiti-app.git
cd bencao-zhiti-app
```

仓库应包含：
- `index.html`          — 完整可运行 APP
- `README.md`           — 产品说明
- `INSTALL.md`          — 本安装指南

## 三、部署到 Vercel 获得在线链接

### 方式 A：GitHub 导入（推荐）
1. 登录 https://vercel.com
2. 点击 New Project
3. 导入 `sandy01384007/bencao-zhiti-app` 仓库
4. Framework Preset 选择 **Other**
5. Build Command 留空，Output Directory 留空
6. 点击 Deploy
7. 部署完成后获得类似 `https://bencao-zhiti-app.vercel.app` 的链接

### 方式 B：拖拽部署
1. 把包含 `index.html` 的文件夹直接拖到 Vercel 网页端
2. 自动部署完成

### 方式 C：Vercel CLI
```bash
npm i -g vercel
vercel
# 按提示登录并部署
```

## 四、手机测试建议

1. 打开在线链接或本地服务
2. 浏览器菜单 → 添加到主屏幕
3. 测试路径：
   - 首页 → AI舌诊 → 选择图片 → 开始分析 → 查看报告 → 存入档案
   - 九种体质自测问卷 → 完成 → 查看雷达图
   - 知识库 / 报告 / 我的 Tab 切换

## 五、接入真实 AI 舌诊模型（进阶）

当前为模拟结果。正式产品推荐：

1. 后端部署开源项目：
   https://github.com/TonguePicture-SKaRD/TongueDiagnosis
   （YOLOv5 定位 + SAM 分割 + ResNet 分类 + LLM 解读）

2. 前端修改 `startAnalyze` 函数，改为调用后端 `/api/tongue/analyze` 接口，把返回结果映射到现有报告结构。

3. 保持免责声明与本地档案逻辑不变。

## 六、转成 React / Vue 正式项目

推荐技术栈：Vite + React + TypeScript

目录建议：
```
src/
├── components/
├── pages/
├── services/tongueApi.ts
├── data/
└── styles/
```

可直接从 `index.html` 中抽取业务逻辑与数据。

## 七、风险与合规提醒

- 所有页面必须保留「本结果仅为养生参考，不构成医疗诊断」声明
- 禁止输出疾病诊断字眼
- 不接入问诊、不开处方、不卖药
- 图片仅用于分析，不公开

## 八、常见问题

**Q：为什么舌诊结果是随机的？**  
A：当前为演示模拟，方便全流程测试。正式版需接真实视觉模型。

**Q：数据存在哪里？**  
A：浏览器 localStorage，清除缓存会丢失。正式版可接入云端数据库。

**Q：如何修改主色？**  
A：搜索 CSS 中的 `--primary: #4A7C59` 即可统一替换。

---
本草知体 · 让中医养生更简单
