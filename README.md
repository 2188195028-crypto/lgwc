<p align="center">
  <img src="https://img.shields.io/badge/Design-Apple_Minimalism-C49A76?style=for-the-badge" alt="Design Style">
  <img src="https://img.shields.io/badge/Type-Product_Page-2C2416?style=for-the-badge" alt="Type">
  <img src="https://img.shields.io/badge/Stack-Vanilla_HTML/CSS/JS-4a6cf7?style=for-the-badge" alt="Stack">
  <img src="https://img.shields.io/badge/Live-GitHub_Pages-27ae60?style=for-the-badge" alt="Live Demo">
</p>

<h1 align="center">理工文创小物商店</h1>
<h3 align="center">Ligong Cultural & Creative Shop</h3>

<p align="center">
  <b>陕西理工大学 · 文创商品单页电商</b><br>
  <sub>Apple 风格极简设计 × 双角色系统（消费者 / 管理者） × 零框架纯原生实现</sub>
</p>

---

## 🎨 设计价值（Design Highlights）

> 作为一个**视觉传达**项目，这个作品的每一个像素都经过设计推敲。

### 配色系统（Design Tokens）
```
米白     #FAF7F2  —  页面基底，温暖克制的"纸色"
浅灰     #F0EDE8  —  卡片与交互区，层次柔和
玫瑰金   #C49A76  —  品牌强调色，贯穿按钮/徽章/边框
深棕     #2C2416  —  文字主色，比纯黑更温润
```
全部颜色通过 CSS 变量（`:root`）集中管理，**支持一键换肤**。

### 视觉语言
| 维度 | 实现 |
|------|------|
| **排版** | Inter（UI 正文）+ Noto Serif SC（标题衬线），Google Fonts CDN |
| **质感** | 玻璃拟态（backdrop-filter blur）+ 5 级阴影层级（xs → xl） |
| **圆角** | 8px → 32px 五级体系，统一圆润感受 |
| **动效** | cubic-bezier 缓出曲线 + 购物车涟漪动画 + 卡片滚动揭示 |
| **响应式** | 桌面 3 列 → 平板 2 列 → 手机 2 列，触摸目标 ≥ 44px |

### 交互细节
- 🛒 购物车 + 按钮 → ✓ 成功闪变 → 数量选择器，完整的状态转换链
- 🎠 Banner 轮播：scroll-snap + 指示点 + 左右箭头 + 键盘方向键，四种操作方式
- 📲 徽标弹跳动画（bump）给予即时操作反馈
- 🔔 Toast 轻提示，圆角胶囊，0.4s 缓出

---

## 🏗 双版本架构

```
├── index.html    ← 🛍 消费者版本（1592 行）
│                   公开面客：浏览 / 搜索 / 分类 / 购物车 / 结算
│                   零编辑入口，零 localStorage 依赖
│
└── admin.html    ← 🔐 管理者版本（2899 行）
                    密码登录门控 → 全功能后台
                    商品 CRUD / 分类管理 / Banner 管理 / JSON 导入导出
                    localStorage 自动持久化
```

| 对比维度 | 消费者版 | 管理者版 |
|----------|:--------:|:--------:|
| 浏览选购 | ✅ | ✅ |
| 购物车结算 | ✅ | ✅ |
| 响应式适配 | ✅ | ✅ |
| 密码登录 | — | 🔐 `admin888` |
| 商品增删改 | — | ✅ |
| 分类管理 | — | ✅ |
| Banner 编辑 | — | ✅ |
| 图片上传(base64) | — | ✅ |
| JSON 导入导出 | — | ✅ |
| 数据持久化 | — | ✅ localStorage |
| Ctrl+E 快捷键 | — | ✅ |

---

## 🔗 在线演示

| 版本 | 链接 |
|------|------|
| 🛍 消费者版 | [**在线访问**](https://2188195028-crypto.github.io/lgwc/) |
| 🔐 管理者版 | [**在线访问**](https://2188195028-crypto.github.io/lgwc/admin.html) |
| 🔑 管理密码 | `admin888` |

> 管理者登录状态保存在 sessionStorage，关闭标签页即自动退出，安全放心。

---

## 🧠 技术亮点（For Developers）

```yaml
架构: 单文件 SPA（零 npm install / 零构建 / 双击即用）
数据流: 数组驱动渲染 → 单向数据流（改数据 → 重渲染）
持久化: localStorage 自动保存（管理端），消费者端无状态
状态管理: 购物车 cart[] / 筛选 activeCategory / 登录 sessionStorage
CSS 架构:
  - 14 节分区注释（变量 → 重置 → 导航 → ... → 登录门控）
  - 全部颜色通过 var() 引用，零硬编码色值
  - Flexbox + Grid 现代布局，零 float
兼容性: Blink / WebKit / Gecko 全兼容，IE11 除外
```

### 代码分区规范
```
<script>
  ├── 密码门控（仅 admin）
  ├── 数据层（products / categories / banners）
  ├── 状态层（cart / activeCategory）
  ├── DOM 引用
  ├── 工具函数
  ├── 渲染层（商品卡片 / Banner / 分类标签）
  ├── 事件绑定（购物车 / 分类筛选 / Banner 轮播）
  ├── 结算栏 & Toast & 购物车抽屉
  └── 管理面板 & 编辑弹窗（仅 admin）
```

---

## 📂 项目结构

```
lgwc/
├── index.html          # 🛍  消费者版（1592 行）
├── admin.html          # 🔐  管理者版（2899 行）
├── 404.html            # CDN 回退加载页
├── app.js              # CDN 分发加载器
├── .cnb.yml            # CNB CloudApp 部署配置
├── .netlify/           # Netlify 部署配置
└── README.md           # 📖 本文档
```

---

## 🚀 快速开始

```bash
# 1. 克隆仓库
git clone git@github.com:2188195028-crypto/lgwc.git

# 2. 直接双击 index.html 或 admin.html 即可运行
#    无需 npm install，无需启动服务器

# 3. 或在本地启动一个静态服务（可选）
npx serve .
# 消费者版: http://localhost:3000
# 管理者版: http://localhost:3000/admin.html
```

---

## 📝 迭代记录

| 版本 | 日期 | 更新内容 |
|------|------|----------|
| v1 | 2026-05-31 | 初始版本：单品页 + 购物车 + Banner |
| v2 | 2026-05-31 | 管理面板 + 商品编辑 + 图片上传 |
| v3 | 2026-06-23 | 双版本拆分 + 密码门控 + 导出导入 + 响应式完善 |

---

<p align="center">
  <sub>Made with ❤️ for 陕西理工大学 · 文创设计</sub><br>
  <sub>Design & Code by <b>Ligong-Wenchang</b> · Powered by Claude Code</sub>
</p>
