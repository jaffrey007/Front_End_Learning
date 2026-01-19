请列出wxml和html的常见对应的标签？

WXML（WeChat Mini Program Markup Language）和 HTML 的常见对应标签如下：

## 基础结构标签
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<view>` | `<div>` | 容器/视图容器 |
| `<text>` | `<span>` | 文本容器 |
| `<block>` | 模板标签（如 `<template>` 或无对应） | 逻辑块，不渲染 |
| `<template>` | `<template>` | 定义模板 |

## 表单相关
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<button>` | `<button>` | 按钮 |
| `<form>` | `<form>` | 表单容器 |
| `<input>` | `<input>` | 输入框 |
| `<textarea>` | `<textarea>` | 多行文本输入 |
| `<label>` | `<label>` | 标签 |
| `<picker>` | `<select>` 或 `<input type="date">` 等 | 选择器 |
| `<slider>` | `<input type="range">` | 滑动选择器 |
| `<switch>` | `<input type="checkbox">`（样式不同） | 开关 |

## 媒体内容
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<image>` | `<img>` | 图片 |
| `<video>` | `<video>` | 视频 |
| `<audio>` | `<audio>` | 音频 |
| `<camera>` | 无直接对应（需JS API） | 相机 |

## 导航与链接
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<navigator>` | `<a>` | 页面链接/导航 |
| `<a>` | 不支持 | 微信小程序中不可用 |

## 列表与表格
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<scroll-view>` | `<div style="overflow:scroll">` | 可滚动区域 |
| `<swiper>` | 轮播插件（如Swiper.js） | 轮播容器 |
| `<list>` | 无直接对应 | 列表（旧版，现推荐用`view`+`wx:for`） |
| 使用 `wx:for` 的 `view` | `<ul>` + `<li>` | 列表渲染 |

## 画布与地图
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<canvas>` | `<canvas>` | 画布 |
| `<map>` | 无直接对应（需地图API） | 地图 |

## 其他
| **WXML 标签** | **HTML 对应标签** | **主要用途** |
|--------------|------------------|-------------|
| `<icon>` | `<i>` + 图标库 | 图标 |
| `<progress>` | `<progress>` | 进度条 |
| `<rich-text>` | `v-html` / `innerHTML` | 富文本渲染 |
| `<web-view>` | `<iframe>` | 内嵌网页 |

## 重要区别：
1. **语义化标签**：HTML5有 `<header>`, `<footer>`, `<section>` 等语义标签，WXML只有 `<view>`
2. **样式单位**：WXML推荐使用 `rpx`（响应式像素），HTML使用 `px`, `em`, `rem` 等
3. **事件绑定**：WXML用 `bindtap`、`catchtap`，HTML用 `onclick`
4. **数据绑定**：WXML用 `{{}}` 语法，HTML原生不支持（需配合JS框架）
5. **列表渲染**：WXML用 `wx:for`，HTML无原生对应
6. **条件渲染**：WXML用 `wx:if`，HTML无原生对应

## 注意事项：
- 小程序中 **没有** `<div>`、`<span>`、`<p>`、`<ul>`、`<li>` 等传统HTML标签
- 所有内容必须包裹在WXML提供的标签内
- 样式写在对应的WXSS文件中，语法类似CSS但有少量差异