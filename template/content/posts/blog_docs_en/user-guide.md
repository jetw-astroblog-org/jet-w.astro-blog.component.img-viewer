---
title: Image Viewer
description: Image Viewer User Guide
pubDate: 2026-03-04
author: jet-w
categories:
  - Documentation
tags:
  - ImageViewer
  - Component
  - Vue
star: true
---

# ImageViewer User Guide

ImageViewer is a Vue component for browsing, filtering, and presenting images with category-based filtering, multiple layout modes, and keyboard navigation.

## Installation

```bash
npm install @jet-w/astro-blog.component.img-viewer
```

## Basic Usage

### In an Astro page (`.astro`)

```astro
---
import ImageViewer from '@jet-w/astro-blog.component.img-viewer/components/ImageViewer.vue';

const images = [
  {
    src: 'https://example.com/photo1.jpg',
    title: 'Sunset Over Mountains',
    categories: ['image'],
    description: 'A beautiful <span class="hi">sunset</span> captured at golden hour.',
  },
  {
    src: 'https://example.com/chart1.jpg',
    title: 'Sales Report Q3',
    categories: ['graph'],
  },
];
---

<ImageViewer client:load images={images} />
```

### In an MDX page (`.mdx`)

```mdx
import ImageViewer from '@jet-w/astro-blog.component.img-viewer/components/ImageViewer.vue';

export const images = [
  {
    src: 'https://example.com/photo1.jpg',
    title: 'Sunset Over Mountains',
    categories: ['image'],
  },
];

<ImageViewer client:load images={images} />
```

::: tip MDX Note
In MDX files, use `export const` instead of `const`. TypeScript type annotations are not supported in MDX.
:::

## Image Data Structure

Each image object supports the following fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `src` | `string` | Yes | Image URL |
| `title` | `string` | Yes | Display title |
| `categories` | `string[]` | No | Category tags for filtering |
| `description` | `string` | No | Description text, supports HTML |

### Example

```js
{
  src: '/images/architecture-diagram.png',
  title: 'System Architecture',
  categories: ['flowchart', 'important'],
  description: 'The diagram shows the <span class="hi">microservice architecture</span> with message queues.',
}
```

An image can belong to multiple categories. The built-in categories are:

- `important`
- `graph`
- `flowchart`
- `map`
- `image`

## Features

### Category Filtering

The toolbar displays filter buttons for each category with a count badge. Click to toggle filters. Multiple categories can be active simultaneously. Click **All** to clear all filters.

### Layout Modes

Two layout modes are available via the layout toggle button in the toolbar:

- **Stack** (default) — description appears below the image
- **Side** — image and description are displayed side by side (max-width expands to 1400px)

### Zoom

Click the zoom button to toggle between 95% and 100% max-width for the displayed image.

### Full Page Mode

Click the full-page button or press `F` to enter full-page mode, which overlays the viewer on top of the page. Press `Escape` to exit.

### Fullscreen

Click the fullscreen button to enter browser native fullscreen with a dark background.

### Random Mode

Click the shuffle button to enable random navigation. When active, next/prev actions jump to a random image instead of sequential order.

### Description Panel

If an image has a `description` field, a **Show/Hide** toggle button appears. The description supports HTML content. Use `<span class="hi">text</span>` to highlight key terms in amber/orange.

### Dark Mode

The component automatically adapts when the parent page uses the `.dark` class on an ancestor element. Fullscreen mode always uses a dark theme.

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `←` | Previous image |
| `→` | Next image |
| `Space` / `↑` / `↓` | Toggle description |
| `F` | Toggle full-page mode |
| `Escape` | Exit full-page mode |

You can also click the left or right half of the image to navigate.

## Navigation

- **Click left half** of the image to go to the previous image
- **Click right half** of the image to go to the next image
- Navigation wraps around (last image goes back to first)
