# 智慧城市大气环境监测大屏（Vue3）

大三寒假实训作品，2026 年 1 月完成。

## 项目简介

一个数据可视化大屏，用 Vue3 搭建，接入高德地图 3D 视图标注监测点位，配合 G2Plot 图表展示空气质量数据。

## 页面结构

大屏由以下组件拼装（`src/pages/components/`）：

| 组件 | 位置 | 说明 |
|---|---|---|
| `Title.vue` | 顶部 | 标题栏 |
| `Map.vue` | 中央 | 高德地图 3D 视图，标注监测点位 |
| `Left1.vue` / `Left2.vue` | 左侧 | 左侧图表区 |
| `Right1.vue` / `Right2.vue` | 右侧 | 右侧图表区 |
| `Bottom1.vue` ~ `Bottom4.vue` | 底部 | 底部四块指标区 |

## 技术栈

- Vue 3 + Vite
- 高德地图 JS API 2.0（`@amap/amap-jsapi-loader`，3D 视图、俯仰角、旋转）
- @antv/g2plot 2.x（图表）
- Less（样式，含大屏背景贴图）

## 运行

```bash
npm install
npm run dev
```

## 注意

`src/pages/components/Map.vue` 中的高德地图 key 为当时实训申请的 web 端 key，可能已失效。自己运行时需在高德开放平台申请新的 Web 端 key 替换。

## 说明

本项目为课程实训，纯前端，无后端接口，数据为静态模拟数据。
