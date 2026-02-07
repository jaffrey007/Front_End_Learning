# 前端样式开发入门必懂知识点

## 一、基础概念与术语

### 1.1 CSS是什么？
- **Cascading Style Sheets**（层叠样式表）
- 用于描述HTML文档的**外观和格式**
- **结构与样式分离**：HTML负责结构，CSS负责表现

### 1.2 样式引入方式
```html
<!-- 1. 内联样式（不推荐，优先级最高） -->
<div style="color: red; font-size: 16px;">内联样式</div>

<!-- 2. 内部样式表（适合小项目） -->
<head>
  <style>
    .box { color: blue; }
  </style>
</head>

<!-- 3. 外部样式表（最佳实践，推荐使用） -->
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

### 1.3 CSS语法结构
```css
/* 选择器 { 属性: 值; } */
选择器 {
  属性1: 值1;  /* 声明 */
  属性2: 值2;
}

/* 示例 */
h1 {
  color: #333;
  font-size: 24px;
  text-align: center;
}
```

## 二、核心选择器系统

### 2.1 基础选择器
```css
/* 1. 元素选择器 */
p { color: blue; }
div { padding: 10px; }

/* 2. 类选择器（最常用） */
.class-name { color: red; }
<div class="class-name"></div>

/* 3. ID选择器（唯一性） */
#unique-id { color: green; }
<div id="unique-id"></div>

/* 4. 通配符选择器 */
* { margin: 0; padding: 0; } /* 重置所有元素边距 */
```

### 2.2 组合选择器
```css
/* 1. 后代选择器（空格） */
.container p { color: gray; } /* .container下的所有p */

/* 2. 子元素选择器（>） */
.container > p { color: blue; } /* 直接子元素p */

/* 3. 相邻兄弟选择器（+） */
h1 + p { margin-top: 0; } /* 紧跟在h1后的p */

/* 4. 通用兄弟选择器（~） */
h1 ~ p { color: red; } /* h1后面所有的p */

/* 5. 并集选择器（,） */
h1, h2, h3 { font-family: Arial; }
```

### 2.3 属性选择器
```css
/* 存在属性 */
[disabled] { opacity: 0.5; }

/* 属性等于特定值 */
[type="text"] { border: 1px solid #ccc; }

/* 属性包含特定值 */
[class*="btn"] { cursor: pointer; }

/* 属性以特定值开头 */
[href^="https"] { color: green; }

/* 属性以特定值结尾 */
[src$=".png"] { border: 2px solid blue; }
```

### 2.4 伪类与伪元素
```css
/* 伪类 - 元素的状态 */
a:hover { color: red; }           /* 鼠标悬停 */
input:focus { border-color: blue; } /* 获得焦点 */
li:first-child { font-weight: bold; } /* 第一个子元素 */
li:nth-child(2n) { background: #f5f5f5; } /* 偶数项 */

/* 伪元素 - 创建虚拟元素 */
p::before { content: "★ "; }     /* 在前面插入内容 */
p::after { content: " !"; }       /* 在后面插入内容 */
p::first-line { font-size: 1.2em; } /* 第一行样式 */
```

## 三、盒模型（Box Model）★

### 3.1 盒模型组成
```
┌─────────────────────────────┐
│          margin             │
│  ┌───────────────────────┐  │
│  │       border          │  │
│  │  ┌─────────────────┐  │  │
│  │  │    padding      │  │  │
│  │  │  ┌───────────┐  │  │  │
│  │  │  │  content  │  │  │  │
│  │  │  └───────────┘  │  │  │
│  │  └─────────────────┘  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

### 3.2 标准盒模型 vs 怪异盒模型
```css
/* 标准盒模型（默认） */
.box {
  width: 100px;      /* content宽度 */
  padding: 20px;     /* +40px */
  border: 5px solid; /* +10px */
  margin: 10px;      /* 外边距 */
  /* 总宽度 = 100 + 40 + 10 = 150px */
}

/* 怪异盒模型（更直观） */
.box {
  box-sizing: border-box; /* ★ 现代开发必加 */
  width: 100px;      /* 总宽度（包括padding+border） */
  padding: 20px;     /* content宽度自动减少 */
  border: 5px solid;
  /* 总宽度 = 100px（固定） */
}

/* 全局设置（推荐） */
* {
  box-sizing: border-box;
}
```

## 四、布局系统（Layout）

### 4.1 传统布局方式
```css
/* 1. 文档流（默认） */
/* 块级元素：独占一行，可设置宽高 */
/* 行内元素：不换行，宽高由内容决定 */

/* 2. 浮动（Float） */
.left { float: left; width: 50%; }
.right { float: right; width: 50%; }
.clearfix::after { /* 清除浮动 */
  content: "";
  display: table;
  clear: both;
}

/* 3. 定位（Position） */
.relative { position: relative; } /* 相对定位 */
.absolute { 
  position: absolute; /* 绝对定位 */
  top: 10px;
  left: 20px;
}
.fixed { position: fixed; }    /* 固定定位 */
.sticky { position: sticky; }  /* 粘性定位 */
```

### 4.2 现代布局：Flexbox（弹性盒子）
```css
.container {
  display: flex; /* 开启弹性布局 */
  
  /* 主轴方向 */
  flex-direction: row; /* 默认：水平排列 */
  /* row | row-reverse | column | column-reverse */
  
  /* 主轴对齐 */
  justify-content: center; 
  /* flex-start | flex-end | center | space-between | space-around | space-evenly */
  
  /* 交叉轴对齐 */
  align-items: center;
  /* stretch | flex-start | flex-end | center | baseline */
  
  /* 换行 */
  flex-wrap: wrap;
  /* nowrap | wrap | wrap-reverse */
}

.item {
  /* 项目属性 */
  flex: 1; /* 简写：flex-grow | flex-shrink | flex-basis */
  order: 2; /* 排列顺序 */
  align-self: flex-start; /* 单独对齐 */
}
```

### 4.3 现代布局：Grid（网格布局）
```css
.container {
  display: grid;
  
  /* 定义网格 */
  grid-template-columns: 100px 1fr 2fr; /* 3列 */
  grid-template-rows: 50px 200px;      /* 2行 */
  
  /* 间距 */
  gap: 10px; /* row-gap column-gap */
  
  /* 区域模板 */
  grid-template-areas:
    "header header header"
    "sidebar content content"
    "footer footer footer";
}

.item {
  /* 位置控制 */
  grid-column: 1 / 3; /* 跨列 */
  grid-row: span 2;   /* 跨行 */
  grid-area: header;  /* 指定区域 */
}
```

### 4.4 响应式布局
```css
/* 1. 媒体查询（Media Queries） */
/* 移动优先原则 */
.container { padding: 10px; }

@media (min-width: 768px) { /* 平板 */
  .container { padding: 20px; }
}

@media (min-width: 1024px) { /* 桌面 */
  .container { padding: 30px; }
}

/* 2. 弹性单位 */
.box {
  width: 100%;           /* 百分比 */
  max-width: 1200px;     /* 最大宽度 */
  margin: 0 auto;        /* 水平居中 */
  padding: 2rem;         /* rem：相对于根元素 */
  font-size: 16px;       /* px：固定单位 */
  line-height: 1.5;      /* 无单位：相对于字体大小 */
}

/* 3. 视口单位 */
.header {
  height: 100vh;        /* 100%视口高度 */
  width: 100vw;         /* 100%视口宽度 */
  font-size: 5vmin;     /* 视口中较小尺寸的5% */
}
```

## 五、样式属性分类

### 5.1 文本样式
```css
.text {
  /* 字体 */
  font-family: "Microsoft YaHei", Arial, sans-serif;
  font-size: 16px;
  font-weight: bold; /* normal | bold | 100-900 */
  font-style: italic;
  
  /* 文本 */
  color: #333333;       /* 颜色 */
  text-align: center;   /* 对齐 */
  line-height: 1.6;     /* 行高 */
  text-decoration: none; /* 装饰 */
  text-transform: uppercase; /* 大小写 */
  
  /* 间距 */
  letter-spacing: 1px;  /* 字符间距 */
  word-spacing: 2px;    /* 单词间距 */
}
```

### 5.2 背景与边框
```css
.element {
  /* 背景 */
  background-color: #f0f0f0;
  background-image: url("bg.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover; /* contain | cover | 具体值 */
  
  /* 渐变背景 */
  background: linear-gradient(45deg, red, blue);
  background: radial-gradient(circle, yellow, green);
  
  /* 边框 */
  border: 2px solid #ccc;
  border-radius: 8px;      /* 圆角 */
  box-shadow: 0 2px 10px rgba(0,0,0,0.1); /* 阴影 */
  
  /* 轮廓（不同于border） */
  outline: 2px dashed red; /* 不占据空间 */
}
```

### 5.3 定位与层级
```css
.box {
  position: relative;
  top: 10px;
  left: 20px;
  z-index: 10; /* 堆叠顺序，越大越靠前 */
  
  /* 显示与隐藏 */
  display: block; /* block | inline | inline-block | none | flex | grid */
  visibility: visible; /* visible | hidden | collapse */
  opacity: 0.8; /* 透明度 0-1 */
  
  /* 溢出处理 */
  overflow: hidden; /* visible | hidden | scroll | auto */
  text-overflow: ellipsis; /* 文本溢出显示... */
  white-space: nowrap; /* 不换行 */
}
```

### 5.4 变换与动画
```css
/* 变换（Transform） */
.transform {
  transform: translate(50px, 100px); /* 移动 */
  transform: rotate(45deg);          /* 旋转 */
  transform: scale(1.5);             /* 缩放 */
  transform: skew(30deg);            /* 倾斜 */
  
  /* 组合变换 */
  transform: translateX(50px) rotate(45deg) scale(1.2);
  
  /* 3D变换 */
  transform: perspective(500px) rotateY(45deg);
}

/* 过渡（Transition） */
.transition {
  transition: all 0.3s ease-in-out;
  /* 简写：property duration timing-function delay */
  
  /* 分解写法 */
  transition-property: width, height;
  transition-duration: 0.5s;
  transition-timing-function: ease-in;
  transition-delay: 0.2s;
}

/* 动画（Animation） */
@keyframes slideIn {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}

.animated {
  animation: slideIn 1s ease-out;
  /* 简写：name duration timing-function delay iteration-count direction */
  
  animation-name: slideIn;
  animation-duration: 1s;
  animation-timing-function: ease;
  animation-iteration-count: infinite; /* 循环次数 */
  animation-direction: alternate;      /* 方向 */
  animation-fill-mode: forwards;       /* 结束后状态 */
}
```

## 六、CSS单位系统

### 6.1 绝对单位
```css
.pixel { font-size: 16px; }  /* 最常用 */
.cm { width: 10cm; }         /* 厘米 */
.mm { width: 100mm; }        /* 毫米 */
.in { width: 1in; }          /* 英寸 = 96px */
.pt { font-size: 12pt; }     /* 点 = 1/72in */
```

### 6.2 相对单位
```css
/* 相对于父元素 */
.percent { width: 50%; }     /* 百分比 */

/* 相对于字体大小 */
.em { font-size: 1.5em; }    /* 相对于当前元素字体 */
.rem { font-size: 1.5rem; }  /* 相对于根元素(html)字体 */

/* 视口单位 */
.vh { height: 100vh; }       /* 视口高度的1% */
.vw { width: 50vw; }         /* 视口宽度的1% */
.vmin { font-size: 5vmin; }  /* 视口较小尺寸的1% */
.vmax { font-size: 5vmax; }  /* 视口较大尺寸的1% */
```

## 七、重要概念与机制

### 7.1 层叠（Cascading）
**样式来源优先级**（从低到高）：
1. 浏览器默认样式
2. 用户自定义样式
3. 外部样式表
4. 内部样式表
5. 内联样式
6. `!important`（慎用）

### 7.2 特异性（Specificity）
**选择器权重计算**（从高到低）：
```
!important > 内联样式 > ID选择器 > 类/伪类/属性 > 元素/伪元素 > 通配符
```
**权重值计算**（具体值）：
- 内联样式：1000
- ID选择器：100
- 类/伪类/属性选择器：10
- 元素/伪元素选择器：1
- 通配符/组合符：0

### 7.3 继承（Inheritance）
```css
/* 可继承的属性 */
font-family, font-size, font-weight
color, text-align, line-height
visibility, cursor

/* 不可继承的属性 */
width, height, margin, padding
border, background, position
display, float, clear
```

## 八、现代CSS特性

### 8.1 CSS变量（Custom Properties）
```css
:root { /* 定义在根元素，全局可用 */
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --spacing-unit: 8px;
}

.element {
  color: var(--primary-color);
  padding: calc(var(--spacing-unit) * 2);
  
  /* 默认值 */
  background: var(--custom-bg, #f0f0f0);
}
```

### 8.2 现代选择器
```css
/* :is() - 简化选择器列表 */
:is(h1, h2, h3) { margin-top: 1em; }

/* :where() - 零特异性选择器 */
:where(h1, h2, h3) { margin-top: 1em; }

/* :has() - 父元素选择器（较新） */
div:has(> p) { border: 1px solid blue; }
```

## 九、最佳实践与常见问题

### 9.1 样式重置与标准化
```css
/* 重置样式 */
* { margin: 0; padding: 0; box-sizing: border-box; }

/* 更好的做法：使用normalize.css或reset.css */
/* 解决浏览器默认样式差异 */
```

### 9.2 BEM命名规范（推荐）
```css
/* Block（块） */
.header { }

/* Element（元素） */
.header__logo { }
.header__nav { }

/* Modifier（修饰符） */
.header--dark { }
.button--disabled { }
```

### 9.3 性能优化
```css
/* 1. 避免使用通配符*选择器 */
/* 2. 减少选择器嵌套深度 */
/* 3. 避免使用@import（影响加载） */
/* 4. 使用transform和opacity实现动画(性能更好) */
/* 5. 压缩和合并CSS文件 */
```

### 9.4 常见布局问题解决方案
```css
/* 1. 水平居中 */
.center-horizontally {
  margin: 0 auto; /* 块级元素 */
  text-align: center; /* 文本和行内元素 */
}

/* 2. 垂直居中 */
.center-vertically {
  /* Flexbox方案（推荐） */
  display: flex;
  align-items: center;
  justify-content: center;
  
  /* Grid方案 */
  display: grid;
  place-items: center;
  
  /* 传统方案 */
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}

/* 3. 等高列 */
.equal-height {
  display: flex; /* 自动等高 */
}
```

## 十、学习路径建议

### 入门阶段（1-2周）
1. **盒模型**、**选择器**、**常用属性**
2. **Flexbox**基础布局
3. **媒体查询**实现响应式

### 进阶阶段（2-4周）
1. **Grid**复杂布局
2. **CSS动画**与**变换**
3. **预处理语言**（Sass/Less）
4. **CSS模块化**与架构

### 实战阶段（持续）
1. 参与实际项目
2. 学习CSS框架（Bootstrap, Tailwind）
3. 关注CSS新特性
4. 性能优化实践

## 总结要点

1. **理解盒模型**：`box-sizing: border-box`
2. **掌握选择器**：理解特异性和继承
3. **熟练Flexbox/Grid**：现代布局的核心
4. **响应式设计**：移动优先，媒体查询
5. **代码组织**：BEM命名，模块化思维
6. **性能意识**：减少重绘，优化动画

CSS看似简单，但深度和细节很多。建议**边学边练**，通过实际项目巩固知识。可以从简单的页面开始，逐步增加复杂度。

test