# 微信公众号编辑器HTML/CSS支持规则

基于实际测试总结的微信公众号编辑器支持的HTML和CSS规则。

## 一、核心原则

### 1. 必须使用内联样式
❌ **不支持**：`<style>` 标签内的CSS
✅ **支持**：所有样式必须写在 `style` 属性中

```html
<!-- 正确写法 -->
<section style="color: #333; font-size: 16px;">

<!-- 错误写法 -->
<style>
    .title { color: #333; }
</style>
<section class="title">
```

### 2. 支持的HTML标签

| 标签 | 支持情况 | 说明 |
|------|---------|------|
| `<section>` | ✅ 完全支持 | **推荐使用**，公众号官方标签 |
| `<div>` | ✅ 支持 | 可用但不如section稳定 |
| `<p>` | ✅ 支持 | 段落文本必须用p包裹 |
| `<span>` | ✅ 支持 | 内联文本样式，可添加 `leaf` 属性 |
| `<h1>` | ✅ 支持 | 文章标题 |
| `<a>` | ✅ 支持 | 链接标签，使用 `href="javascript:void(0);"` |
| `<em>` | ✅ 支持 | 强调文本，用于元数据 |
| `<svg>` | ✅ 支持 | 可作为占位符使用，支持嵌套和动画 |
| `<img>` | ✅ 支持 | 图片标签，支持多个数据属性 |
| `<animate>` | ✅ 支持 | SVG动画标签 |
| `<foreignObject>` | ✅ 支持 | SVG中嵌入HTML |
| `<table>` | ⚠️ 部分支持 | 不推荐使用 |
| `<button>` | ❌ 不支持 | 会被过滤 |

## 二、CSS属性

### 1. 基础属性
```css
box-sizing: border-box;      /* 确保盒模型一致 */
visibility: visible;         /* 确保元素可见 */
```

### 2. 文本相关
```css
font-style: normal;
font-weight: 400;
text-align: justify;        /* 两端对齐 */
font-size: 16px;
color: rgb(62, 62, 62);
line-height: 2;
white-space: normal;        /* 确保文本正常换行 */
text-indent: 2em;           /* 首行缩进 */
```

### 3. 布局相关
```css
display: flex;               /* Flexbox布局 */
justify-content: center;
align-items: center;
flex-flow: row;             /* 或 column */
align-self: flex-start;
width: 100%;
max-width: 677px;           /* 公众号标准宽度 */
```

#### 3.1 百分比单位支持

微信公众号编辑器完全支持百分比单位，推荐使用百分比实现响应式布局。

```css
/* 宽度 */
width: 100%;
max-width: 100%;

/* 边距（推荐使用百分比实现响应式） */
margin: 15px 0%;           /* 上下15px，左右0% */
padding: 0px 3%;           /* 左右3%内边距 */
max-width: 100%;           /* 响应式最大宽度 */

/* 百分比布局示例 */
<section style="max-width: 100%; margin: 15px 0%;">
    <section style="padding: 0px 3%;">
        内容
    </section>
</section>
```

### 4. 间距和边框
```css
margin: 10px 0px;
padding: 20px 25px;
border: 1px solid #667eea;
border-left: 4px solid #667eea;
border-radius: 8px;
```

### 5. 背景和装饰
```css
background-color: #f8f9ff;
background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);  /* 可能被过滤 */
```

### 6. 特殊效果
```css
/* 变换（部分支持） */
transform: rotateZ(45deg);
-webkit-transform: rotateZ(45deg);
transform: perspective(0px);

/* 过渡（可能被过滤） */
transition: all 0.2s;
```

## 三、布局策略

### 1. 容器结构
```html
<section style="box-sizing: border-box; visibility: visible;">
    <!-- 内容 -->
</section>
```

### 2. 段落布局
```html
<section style="box-sizing: border-box; visibility: visible; padding: 0px 25px; margin-bottom: 25px;">
    <p style="text-indent: 2em; white-space: normal; margin: 0px; padding: 0px; box-sizing: border-box; visibility: visible; color: #3a3a3a; line-height: 2;">
        文本内容...
    </p>
</section>
```

### 3. 引用框布局
```html
<section style="box-sizing: border-box; visibility: visible; padding: 0px 25px;">
    <section style="text-align: left; justify-content: flex-start; display: flex; flex-flow: row; margin: 0px; width: 100%; background-color: #f8f9ff; padding: 20px 25px; border-left: 4px solid #667eea; box-sizing: border-box;">
        <section style="text-align: justify; width: 100%; box-sizing: border-box;">
            <p style="text-indent: 0; color: #3a3a3a; line-height: 2;">
                引用内容...
            </p>
        </section>
    </section>
</section>
```

### 4. 分割线
```html
<section style="margin: 10px 0px; box-sizing: border-box; visibility: visible;">
    <section style="background-color: #e0e0e0; height: 1px; box-sizing: border-box;"></section>
</section>
```

## 四、颜色规范

### 1. 支持的颜色格式
```css
/* 十六进制 */
color: #667eea;

/* RGB */
color: rgb(62, 62, 62);

/* RGBA（部分支持） */
color: rgba(102, 126, 234, 0.1);

/* 渐变 */
background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
```

### 2. 推荐配色方案
```css
/* 主色调 */
color: #667eea;              /* 蓝紫色 */
background-color: #667eea;

/* 文本色 */
color: #2c3e50;              /* 深色标题 */
color: #3a3a3a;              /* 正文 */
color: #7f8c8d;              /* 副标题 */
color: #999999;              /* 辅助文本 */

/* 背景色 */
background-color: #f8f9ff;   /* 浅蓝背景 */
background-color: #f0f4ff;   /* 提示背景 */
```

## 五、不支持的特性

### 1. CSS选择器
❌ 类选择器 `.class`
❌ ID选择器 `#id`
❌ 属性选择器 `[attr]`
❌ 伪类 `:hover`, `:focus`
❌ 伪元素 `::before`, `::after`

### 2. 定位
❌ `position: absolute`
❌ `position: fixed`
❌ `position: relative` (部分支持)

### 3. 复杂效果
❌ `box-shadow` (会被过滤)
❌ `filter` (会被过滤)
❌ `animation` (会被过滤)
❌ `transition` (会被过滤)

## 六、最佳实践

### 1. 使用section标签
```html
<!-- ✅ 推荐 -->
<section style="...">内容</section>

<!-- ⚠️ 可以用但不推荐 -->
<div style="...">内容</div>
```

### 2. 段落必须用p标签
```html
<!-- ✅ 正确 -->
<p style="text-indent: 2em;">段落内容</p>

<!-- ❌ 错误 -->
<section style="text-indent: 2em;">段落内容</section>
```

### 3. 嵌套section实现布局
```html
<section style="display: flex; flex-flow: row;">
    <section style="flex: 1;">左侧内容</section>
    <section style="flex: 1;">右侧内容</section>
</section>
```

### 4. 每个元素都添加关键属性
```html
<section style="
    box-sizing: border-box;
    visibility: visible;
    /* 其他样式 */
">
```

## 七、复制粘贴技巧

### 1. 从网页复制到公众号
1. 选中内容（Ctrl+A）
2. 复制（Ctrl+C）
3. 在公众号编辑器中粘贴（Ctrl+V）
4. 检查格式是否正确

### 2. 使用第三方编辑器（推荐）
- 135编辑器：www.135editor.com
- i排版：www.ipaiban.com
- 秀米：xiumi.us

### 3. 调试技巧
```html
<!-- 添加背景色查看布局 -->
<section style="background-color: red;">

<!-- 添加边框查看范围 -->
<section style="border: 1px solid blue;">
```

## 八、完整模板

```html
<section style="box-sizing: border-box; font-style: normal; font-weight: 400; text-align: justify; font-size: 16px; color: rgb(62, 62, 62); margin-bottom: 0px; visibility: visible;">

    <!-- 装饰线 -->
    <section style="margin: 10px 0px 3px; box-sizing: border-box; visibility: visible;">
        <section style="background: linear-gradient(90deg, #667eea 0%, #764ba2 100%); height: 6px; box-sizing: border-box; visibility: visible;"></section>
    </section>

    <!-- 标题 -->
    <section style="text-align: center; font-size: 22px; color: #2c3e50; line-height: 1.6; margin: 25px 0px; box-sizing: border-box; visibility: visible;">
        <p style="margin: 0px; padding: 0px; box-sizing: border-box; visibility: visible;">文章标题</p>
    </section>

    <!-- 正文段落 -->
    <section style="box-sizing: border-box; visibility: visible; padding: 0px 25px; margin-bottom: 25px;">
        <p style="text-indent: 2em; white-space: normal; margin: 0px; padding: 0px; box-sizing: border-box; visibility: visible; color: #3a3a3a; line-height: 2; text-align: justify;">
            正文内容...
        </p>
    </section>

</section>
```

## 九、常见问题

### Q1: 为什么粘贴后样式丢失？
**A**: 检查是否使用了 `<style>` 标签或class选择器，必须使用内联样式。

### Q2: 为什么某些CSS属性不生效？
**A**: 公众号会过滤 `box-shadow`、`filter`、`animation` 等属性。

### Q3: 如何实现复杂布局？
**A**: 使用嵌套的 `<section>` 标签配合 `display: flex`。

### Q4: 图片如何处理？
**A**: 使用 `<img>` 标签，添加 `style="max-width: 100%; width: 100%; box-sizing: border-box;"`

---

## 十、图片处理

### 1. 图片标签完整写法
```html
<img
    data-src="图片URL"
    data-ratio="0.749"
    data-s="300,640"
    data-w="1080"
    class="rich_pages wxw-img"
    style="vertical-align: middle; max-width: 100%; width: 100%; box-sizing: border-box;"
    width="100%"
    alt="图片"
>
```

### 2. 支持的图片属性

| 属性 | 说明 | 示例 |
|------|------|------|
| `data-src` | 图片地址（懒加载） | `data-src="https://..."` |
| `data-ratio` | 宽高比 | `data-ratio="0.749"` |
| `data-s` | 尺寸参数 | `data-s="300,640"` |
| `data-w` | 宽度 | `data-w="1080"` |
| `class` | 样式类 | `rich_pages wxw-img` |
| `width` | 显示宽度 | `width="100%"` |
| `alt` | 替代文本 | `alt="图片"` |

### 3. 图片容器
```html
<section style="text-align: center; margin: 10px 0px; line-height: 0; box-sizing: border-box;">
    <section style="max-width: 100%; vertical-align: middle; display: inline-block; line-height: 0; width: 100%; box-sizing: border-box;">
        <img src="..." style="vertical-align: middle; max-width: 100%; width: 100%; box-sizing: border-box;">
    </section>
</section>
```

## 十一、SVG动画

### 1. SVG基本结构
```html
<svg
    width="100.00%"
    xmlns="http://www.w3.org/2000/svg"
    style="box-sizing: border-box; transform: rotateZ(0deg); width: 100%;"
    viewBox="0 0 1000 720"
    role="img"
    aria-label="插图"
>
    <!-- SVG内容 -->
</svg>
```

### 2. SVG中嵌入图片
```html
<svg x="0%" y="0%" width="100%" xmlns="http://www.w3.org/2000/svg">
    <foreignObject width="100%" height="100%" x="0%" y="0%">
        <svg
            style="display: block; width: 100%; background-image: url('图片URL'); background-size: cover;"
            viewBox="0 0 1000 720"
        >
        </svg>
    </foreignObject>
</svg>
```

### 3. SVG动画
```html
<svg viewBox="0 0 1000 720">
    <animate
        fill="freeze"
        attributeName="opacity"
        begin="click"
        from="1"
        to="0"
        dur="1"
        restart="never"
        elem-animation-type="Fade"
    />
</svg>
```

### 4. 支持的动画属性

| 属性 | 说明 | 值 |
|------|------|-----|
| `attributeName` | 动画属性 | `opacity`, `width` 等 |
| `begin` | 开始时间 | `click`, `click + 1s` |
| `from` | 起始值 | `0`, `1` |
| `to` | 结束值 | `0`, `1` |
| `dur` | 持续时间 | `1`, `0.5` |
| `fill` | 填充模式 | `freeze` |
| `restart` | 重启模式 | `never` |

## 十二、特殊CSS属性

### 1. CSS变量
```css
/* 支持CSS变量 */
text-size-adjust: var(--content-font-scale-percent, inherit);
```

### 2. 特殊属性
```css
/* 字体间距 */
letter-spacing: 0.034em;

/* 宽高比 */
aspect-ratio: calc(3.87597) / 1;

/* 透明度（用于动画） */
opacity: 1;

/* 用户选择 */
user-select: none;

/* 指针事件 */
pointer-events: none;

/* -webkit前缀属性 */
-webkit-tap-highlight-color: transparent;
-webkit-transform: rotateZ(0deg);
```

## 十三、第三方编辑器特殊标记

### 1. SVG布局工具条
```html
<section style="display: inline-block; width: 100%; overflow: hidden; align-self: flex-start;">
    <section style="height: 0px; overflow: visible;">
        <!-- 动画SVG内容 -->
    </section>
    <section style="height: 0px; padding-top: 72%;">
        <!-- 占位SVG -->
    </section>
</section>
```

### 2. 叶子节点标记
```html
<span leaf="">文本内容</span>
<section nodeleaf="">内容</section>
```

### 3. 自动排版类
```html
<div class="autoTypeSetting24psection">
    <!-- 自动排版内容 -->
</div>
```

## 十四、性能优化

### 1. 图片懒加载
```html
<img data-src="图片URL" class="wx_img_placeholder">
```

### 2. 图片占位符
```html
<!-- 使用1x1透明GIF作为占位符 -->
<img src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" class="wx_imgbc_placeholder">
```

### 3. SVG占位
```html
<!-- 使用viewBox="0 0 1 1"的SVG占位 -->
<svg viewBox="0 0 1 1" style="float:left; line-height:0; width:0; vertical-align:top;"></svg>
```

## 十五、完整示例（带图片）

```html
<section style="box-sizing: border-box; visibility: visible;">
    <!-- 标题 -->
    <section style="text-align: center; font-size: 22px; margin: 25px 0px;">
        <p style="margin: 0px; font-weight: bold;">文章标题</p>
    </section>

    <!-- 图片 -->
    <section style="text-align: center; margin: 10px 0px; line-height: 0;">
        <section style="max-width: 100%; vertical-align: middle; display: inline-block; width: 100%;">
            <img
                data-src="https://example.com/image.jpg"
                data-ratio="0.75"
                class="rich_pages wxw-img"
                style="vertical-align: middle; max-width: 100%; width: 100%; box-sizing: border-box;"
                alt="图片"
            >
        </section>
    </section>

    <!-- 正文 -->
    <section style="padding: 0px 25px; margin-bottom: 25px;">
        <p style="text-indent: 2em; line-height: 2; color: #3a3a3a;">
            正文内容...
        </p>
    </section>
</section>
```

---

## 更新日志

- 2025-01-11: 初始版本，基于实际测试总结
- 2025-01-11: 新增图片处理、SVG动画、特殊CSS属性章节