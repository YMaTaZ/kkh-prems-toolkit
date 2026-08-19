# KKH PREMs Toolkits — Resource Hub

KK Women's and Children's Hospital（SingHealth）患者体验（PX）项目工具包展示网站。

**在线站点：** https://ymataz.github.io/kkh-prems-toolkit/

---

## 这个仓库是做什么的

为 PREMs Translation Toolkit 项目提供**面向一线医护与项目相关方的资源展示站**，把三类核心交付物集中呈现：

| 板块 | 内容 | 形式 |
|---|---|---|
| **Resource Guide** | PX Dashboard 资源指南（Filters / Quantitative / Prioritisation 等） | PDF.js 逐页渲染 + 翻页/缩放/跳转 |
| **Checklist** | Dashboard Action Checklist（四步管理循环） | PDF.js 逐页渲染 |
| **Storyboard** | 7 帧使用场景故事板（READ > UNDERSTAND > ACT） | 图集翻页 + 帧号跳转 + 一键打印 |
| **Screenshots** | 10 张 dashboard / resource guide 参考截图 | 图集翻页 + 帧号跳转 |

核心流程：**读懂数据 → 找到重点 → 打印清单 → 团队行动 → 复检**。

## 技术栈

- 纯静态站点：原生 HTML / CSS / JS，零框架、零构建
- PDF 预览：PDF.js（本地自托管 `lib/`），同域加载 assets 仓库的 PDF
- 部署：GitHub Pages + GitHub Actions（`configure-pages` + `upload-pages-artifact` + `deploy-pages`）
- PDF 托管：独立资产仓库 [prems-assets](https://github.com/YMaTaZ/prems-assets)（同域，保证 iframe/PDF.js 可加载且部署轻量）

## 目录结构

```
├── index.html              # 单页应用（四个板块视图切换）
├── lib/                    # PDF.js 本地库
├── storyboard/             # 7 帧故事板图片（1.png ~ 7.png）
├── screenshots/            # 10 张 dashboard 参考截图（01.png ~ 10.png）
└── .github/workflows/      # GitHub Pages 部署工作流
```

PDF 文件不在此仓库，位于 [prems-assets](https://github.com/YMaTaZ/prems-assets)（`resource-guide.pdf` / `checklist.pdf`），配置在 `index.html` 的 `PDF_SOURCES`。

## 如何更新内容

### 更新 PDF（Resource Guide / Checklist）

1. 克隆并推送 `prems-assets` 仓库，替换 `resource-guide.pdf` 或 `checklist.pdf`
2. 等待其 GitHub Pages 自动部署（约 1-2 分钟）
3. **主站无需改动**，预览与下载自动指向最新文件

### 更新故事板 / 截图

- 替换 `storyboard/1.png ~ 7.png`（或 `screenshots/01.png ~ 10.png`）
- 若新增/删减张数，同步更新 `index.html` 中 `STORYBOARD_IMAGES` / `SCREENSHOT_IMAGES` 数组与标题
- push 到 main，Actions 自动部署

## 设计要点

- 视觉：浅色、细边框、轻阴影、简约风；唯一强调色 `#1F4E79 / #2E75B6`
- 动效：视图切换淡入淡出 + 卡片错峰入场 + hover 微交互，支持 `prefers-reduced-motion` 降级
- PDF 性能：fit 模式页缓存 + 相邻页预渲染，翻页秒开；`rangeChunkSize` 256KB 按页拉取

## 版本历史

- `v1-iframe-preview` — iframe 原生 PDF 预览版（留档 tag，可回退）
- 当前 main — PDF.js 同域逐页渲染版

## 隐私声明

站点内容含患者体验数据与内部指南，标注 **Restricted · Sensitive (Normal)**，请勿公开传播原始数据。

---

*HCD Final Project · July 2026 · OPE × SUTD*
