# Fangal

三站聚合的 Galgame（Galgame 视觉小说）桌面应用。将多个来源站的游戏目录合并为一个统一视图，支持搜索、分类筛选、跨站资源聚合、内置下载管理器和一键检查更新。

界面采用现代暗色设计，针对桌面端优化（Windows）。

## 功能特性

- **三站聚合**：整合三个来源站的游戏数据，按规范化标题自动去重归类，同一游戏在不同站点的入口会合并为一条记录，详情页可自由切换来源。
- **搜索与筛选**：支持关键词搜索，以及按类型、语言、平台、标签多维度筛选。
- **分类浏览**：自动提取类型 / 语言 / 平台 / 标签分类，点击分类即可筛选出对应作品。
- **跨站资源整合**：同一游戏可聚合多个站点的可下载资源，一键获取有效下载链接。
- **内置下载管理器**：
  - 多任务并发队列（可配置并发数）
  - HTTP Range 断点续传
  - 暂停 / 恢复 / 取消
  - 实时下载速度与进度
  - 任务持久化，重启后可继续

## 技术栈

- **Electron** 31.x —— 桌面容器
- **React** 18 —— 渲染层
- **Vite** 5 —— 构建工具
- **electron-builder** —— 打包（NSIS 安装包）

## 快速开始（开发）

```bash
# 安装依赖
npm install

# 启动开发模式（同时起 Vite 与 Electron，带热更新）
npm run dev
```

也可以分开启动：

```bash
# 起渲染层
npm run dev:renderer

# 另开终端起 Electron 主进程
npm run dev:electron
```

## 打包

```bash
# 构建并产出 Windows 安装包（NSIS，x64）
npm run build:app

# 只产出解包目录（免安装）
npm run build:dir
```

打包产物输出到 `release/` 目录，安装包文件名为 `Fangal Setup x.y.z.exe`。

## 项目结构

```
galgame-hub/
├─ src/
│  ├─ main/            # 主进程
│  │  ├─ index.js      # 窗口、IPC、生命周期
│  │  ├─ sites.js      # 三站配置
│  │  ├─ dataFetcher.js# 抓取与请求
│  │  ├─ aggregator.js # 聚合、去重、分类、筛选
│  │  ├─ store.js      # 数据编排层
│  │  ├─ downloader.js # 内置下载管理器
│  │  ├─ resourceResolver.js # 资源解析聚合
│  │  ├─ updater.js    # 检查更新（GitHub Releases）
│  │  ├─ settings.js   # 设置持久化
│  │  ├─ cache.js      # 本地缓存
│  │  └─ secure.js     # 安全加固
│  ├─ preload/         # 渲染进程桥接
│  └─ renderer/        # React 界面
│     └─ src/
│        ├─ pages/     # 主页 / 分类 / 详情 / 下载 / 设置
│        ├─ components/# 通用组件
│        └─ styles/    # 样式
├─ build/              # 打包资源（图标、NSIS 配置）
├─ release/            # 打包产物
└─ dist/               # 前端构建输出
```



## 许可证

[MIT](LICENSE)

## 免责声明

本项目仅用于技术学习与个人使用，聚合的数据均来自公开接口。请尊重各来源站点的版权与使用条款，勿将本项目用于商业用途。
