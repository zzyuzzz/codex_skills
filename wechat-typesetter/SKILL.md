---
name: wechat-typesetter
description: >
  微信公众号文章HTML排版工具。将Markdown或纯文本转换为符合微信公众号编辑器规范的富文本HTML。
  当用户需要以下操作时使用此技能：(1) 将Markdown/纯文本转换为微信公众号排版HTML；(2) 生成符合公众号规范的富文本排版代码；
  (3) 排版政务、新闻、科普、通知等各类公众号文章；(4) 对已有HTML进行公众号兼容性检查与修复。
  触发关键词包括："微信公众号排版"、"公众号排版"、"微信排版"、"排版"、"公众号文章"、"微信编辑器"、
  "WeChat article"、"公众号HTML"、"微信富文本"。
---

# 微信公众号排版技能

将 Markdown / 纯文本转换为可直接粘贴到微信公众号编辑器的 HTML 代码。

## 排版流程

### 1. 分析源文档结构

识别以下元素并标记：
- 文章标题、副标题/来源信息
- 章节标题（一级 #、二级 ##、三级 ###）
- 正文段落
- 有序/无序列表
- 引用块
- 图片占位（![alt](url) 或文字描述）
- 表格
- 分割线

### 2. 选择主题配色

根据文章内容类型选择配色方案。支持以下预设主题：

| 主题 | 主色 | 浅底色 | 适用场景 |
|------|------|--------|---------|
| 默认蓝 | #667eea | #f0f4fa | 通用、科技 |
| 红色 | #ba372a | #fef2f2 | 政务、党建、红色主题 |
| 墨绿 | #2d6a4f | #f0faf4 | 环保、健康、中医药 |
| 橙色 | #d97706 | #fffbeb | 教育、安全、警示 |
| 紫色 | #7c3aed | #f5f3ff | 商务、金融、高端 |

用户可自定义主色和浅底色覆盖预设。

### 3. 生成 HTML

使用 ssets/basic-template.html 作为外壳模板，用 ssets/block-templates.html 中的内容块拼接文章内容。

#### 必须遵守的规则

1. **所有样式内联**：每个元素必须有 style 属性，不使用 <style> 标签和 class。
2. **标签选择**：优先使用 <section>，段落用 <p>，内联修饰用 <span>。禁止 <button>。避免 <table>。
3. **盒模型**：所有容器加 ox-sizing: border-box;。
4. **最大宽度**：外层容器 max-width: 677px; margin-left: auto; margin-right: auto;。
5. **字体**：ont-family: 'Microsoft YaHei', sans-serif;。
6. **正文**：ont-size: 16px; line-height: 2; text-indent: 2em; text-align: justify; color: #2b2b2b;。
7. **章节标题**：ont-size: 20px; font-weight: bold;，使用左侧竖线装饰。
8. **百分比布局**：左右边距用 padding: 0 30px;，支持响应式。
9. **图片**：使用三层 section 包裹，width: 100%; max-width: 100%;。
10. **注释标记**：使用 HTML 注释 <!-- 章节标题 --> 标记每个内容块用途。

#### 元素映射规则

| Markdown 元素 | HTML 模板 |
|---------------|-----------|
| # 标题 | 居中标题区 <p style="font-size:24px;font-weight:bold;"> |
| ## 章节标题 | 竖线装饰标题 <section style="border-left:4px solid COLOR"> |
| ### 二级标题 | 底色标题 <section style="background-color:LIGHT_COLOR"> |
| 普通段落 | <p style="text-indent:2em;line-height:2;"> |
| > 引用 | 引用框 <section style="background-color:#f8f9ff;border-left:4px solid COLOR;"> |
| 1. 列表 | 编号圆形标记 |
| - 列表 | 左缩进 + 圆点 |
| ![img](url) | 三层 section 包裹 <img> |
| --- | 1px 灰色分割线 |

#### 输出格式

输出完整的 <!DOCTYPE html> 文档，以 <!-- 标题区 --> 等 HTML 注释标记各区块，便于用户定位和修改。

### 4. 自检清单

生成 HTML 后逐项检查：
- [ ] 无 <style> 标签和 CSS 类
- [ ] 无 <button>, <script>, <iframe>
- [ ] 所有元素有内联 style 属性
- [ ] 外层容器 max-width: 677px
- [ ] 正文 	ext-indent: 2em; line-height: 2
- [ ] 图片有 max-width: 100%
- [ ] 无无效 CSS 属性（如 nimation, @media）

## 参考文档

排版技术规范详见 eferences/wechat-rules.md，包含完整的标签支持列表、CSS 属性兼容性和 SVG 动画说明。

## 模板文件

- ssets/basic-template.html：完整文章外壳模板
- ssets/block-templates.html：各内容块模板（段落、标题、引用、图片、列表等）
