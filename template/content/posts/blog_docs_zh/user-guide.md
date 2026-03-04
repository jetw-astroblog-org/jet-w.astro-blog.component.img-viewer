---
title: ImageViewer 使用指南
description: ImageViewer 图片查看器组件的完整使用指南，包括图片浏览、分类筛选和展示功能。
pubDate: 2025-01-08
author: jet-w
categories:
  - 文档
tags:
  - ImageViewer
  - 组件
  - Vue
star: true
---

# ImageViewer 使用指南

ImageViewer 是一个 Vue 组件，提供图片浏览、分类筛选、多种布局模式和键盘导航等功能。

## 安装

```bash
npm install @jet-w/astro-blog.component.img-viewer
```

## 基本用法

### 在 Astro 页面中 (`.astro`)

```astro
---
import ImageViewer from '@jet-w/astro-blog.component.img-viewer/components/ImageViewer.vue';

const images = [
  {
    src: 'https://example.com/photo1.jpg',
    title: '山间日落',
    categories: ['image'],
    description: '在黄金时段捕捉到的<span class="hi">美丽日落</span>。',
  },
  {
    src: 'https://example.com/chart1.jpg',
    title: '第三季度销售报告',
    categories: ['graph'],
  },
];
---

<ImageViewer client:load images={images} />
```

### 在 MDX 页面中 (`.mdx`)

```mdx
import ImageViewer from '@jet-w/astro-blog.component.img-viewer/components/ImageViewer.vue';

export const images = [
  {
    src: 'https://example.com/photo1.jpg',
    title: '山间日落',
    categories: ['image'],
  },
];

<ImageViewer client:load images={images} />
```

::: tip MDX 注意事项
在 MDX 文件中，需要使用 `export const` 而非 `const`。MDX 不支持 TypeScript 类型注解。
:::

## 图片数据结构

每个图片对象支持以下字段：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `src` | `string` | 是 | 图片 URL |
| `title` | `string` | 是 | 显示标题 |
| `categories` | `string[]` | 否 | 分类标签，用于筛选 |
| `description` | `string` | 否 | 描述文字，支持 HTML |

### 示例

```js
{
  src: '/images/architecture-diagram.png',
  title: '系统架构图',
  categories: ['flowchart', 'important'],
  description: '该图展示了基于消息队列的<span class="hi">微服务架构</span>。',
}
```

每张图片可以属于多个分类。内置分类包括：

- `important` — 重要
- `graph` — 图表
- `flowchart` — 流程图
- `map` — 地图
- `image` — 图片

## 功能介绍

### 分类筛选

工具栏中显示每个分类的筛选按钮，并带有数量标记。点击可切换筛选条件，支持同时选中多个分类。点击 **All** 可清除所有筛选。

### 布局模式

通过工具栏中的布局切换按钮，可以选择两种布局模式：

- **堆叠模式**（默认）— 描述显示在图片下方
- **并排模式** — 图片和描述并排显示（最大宽度扩展至 1400px）

### 缩放

点击缩放按钮可在 95% 和 100% 最大宽度之间切换。

### 全页模式

点击全页按钮或按 `F` 键进入全页模式，查看器将覆盖整个页面。按 `Escape` 退出。

### 全屏模式

点击全屏按钮进入浏览器原生全屏模式，使用深色背景。

### 随机模式

点击随机按钮启用随机浏览。启用后，前进/后退操作将跳转到随机图片，而非按顺序浏览。

### 描述面板

如果图片包含 `description` 字段，会出现 **Show/Hide** 切换按钮。描述支持 HTML 内容，使用 `<span class="hi">文字</span>` 可以用琥珀色高亮关键词。

### 深色模式

当父页面的祖先元素使用了 `.dark` 类时，组件会自动适配深色主题。全屏模式始终使用深色主题。

## 键盘快捷键

| 按键 | 功能 |
|------|------|
| `←` | 上一张图片 |
| `→` | 下一张图片 |
| `Space` / `↑` / `↓` | 切换描述显示 |
| `F` | 切换全页模式 |
| `Escape` | 退出全页模式 |

也可以点击图片的左半部分或右半部分进行导航。

## 导航方式

- **点击图片左半部分** — 切换到上一张图片
- **点击图片右半部分** — 切换到下一张图片
- 导航会循环（最后一张之后回到第一张）
