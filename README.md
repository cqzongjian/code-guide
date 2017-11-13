# 前端编码指南

## 目录 

[1 命名规则](#1)

[2 HTML](#2)

[3 CSS, SCSS](#3)

[4 JavaScript](#4)



----------


<h2 id='1'> 1 命名规则 </h2>

项目、目录、文件名称应该使用小写字符, 以避免在有些系统平台上不识别大小写的命名方式。项目、目录、文件名不要包含除 - 和 _ 外的标点符号。

### 1.1 项目命名

全部采用小写方式， 以下划线分隔。

例：`my_project_name`

### 1.2 目录命名

参照项目命名规则；

有复数结构时，要采用复数命名法。

例：`scripts, styles, images, data_models`

### 1.3 JS文件命名

参照项目命名规则。

例：`account_model.js`

### 1.4 CSS, SCSS文件命名

参照项目命名规则。

例：`retina_sprites.scss`

### 1.5 HTML文件命名

参照项目命名规则。

例：`error_report.html`

----------

<h2 id='2'> 2 HTML </h2>

### 2.1 语法

- 缩进使用soft tab（4个空格）；
- 嵌套的节点应该缩进；
- 在属性上，使用双引号，不要使用单引号；
- 属性名全小写，用中划线做分隔符；
- 不要在自动闭合标签结尾处使用斜线（HTML5 规范 指出他们是可选的）；
- 不要忽略可选的关闭标签，例：`</li>` 和` </body>`。

		<!DOCTYPE html>
		<html>
		    <head>
		        <title>Page title</title>
		    </head>
		    <body>
		        <img src="images/company_logo.png" alt="Company">
		
		        <h1 class="hello-world">Hello, world!</h1>
		    </body>
		</html>

### 2.2 HTML5 doctype

在页面开头使用这个简单地doctype来启用标准模式，使其在每个浏览器中尽可能一致的展现；

虽然doctype不区分大小写，但是按照惯例，doctype大写。

	<!DOCTYPE html>
	<html>
		...
	</html>

### 2.3 lang属性

根据HTML5规范：

> 应在html标签上加上lang属性。这会给语音工具和翻译工具帮助，告诉它们应当怎么去发音和翻译。

更多关于 lang 属性的说明[在这里](http://w3c.github.io/html/semantics.html#the-html-element "在这里")；

在sitepoint上可以查到[语言列表](https://www.sitepoint.com/iso-2-letter-language-codes/ "语言列表")；

但sitepoint只是给出了语言的大类，例如中文只给出了zh，但是没有区分香港，台湾，大陆。而微软给出了一份更加[详细的语言列表](https://msdn.microsoft.com/en-us/library/ms533052(v=vs.85).aspx "详细的语言列表")，其中细分了zh-cn, zh-hk, zh-tw。

	<!DOCTYPE html>
	<html lang="en-us">
	    ...
	</html>

### 2.4 字符编码

通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为'UTF-8'。

	<!DOCTYPE html>
	<html>
	    <head>
	        <meta charset="UTF-8">
	    </head>
	    ...
	</html>

### 2.5 IE兼容模式

用 <meta> 标签可以指定页面应该用什么版本的IE来渲染；

如果你想要了解更多，请点击[这里](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do "这里")；

不同doctype在不同浏览器下会触发不同的渲染模式（[这篇文章](https://hsivonen.fi/doctype/ "这篇文章")总结的很到位）。

	<!DOCTYPE html>
	<html>
	    <head>
	        <meta http-equiv="X-UA-Compatible" content="IE=Edge">
	    </head>
	    ...
	</html>

### 2.6 引入CSS, JS

根据HTML5规范, 通常在引入CSS和JS时不需要指明 type，因为 text/css 和 text/javascript 分别是他们的默认值。

	<!-- External CSS -->
	<link rel="stylesheet" href="code_guide.css">
	
	<!-- In-document CSS -->
	<style>
	    ...
	</style>
	
	<!-- External JS -->
	<script src="code_guide.js"></script>
	
	<!-- In-document JS -->
	<script>
	    ...
	</script>

### 2.7 属性顺序

属性应该按照特定的顺序出现以保证易读性；

- class
- id
- name
- data-*
- src, for, type, href, value , max-length, max, min, pattern
- placeholder, title, alt
- aria-*, role
- required, readonly, disabled

class是为高可复用组件设计的，所以应处在第一位；

id更加具体且应该尽量少使用，所以将它放在第二位。

	<a class="..." id="..." data-modal="toggle" href="#">Example link</a>
	
	<input class="form-control" type="text">
	
	<img src="..." alt="...">

### 2.8 boolean属性

boolean属性指不需要声明取值的属性，XHTML需要每个属性声明取值，但是HTML5并不需要；

更多内容可以参考 [WhatWG section on boolean attributes](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes "WhatWG section on boolean attributes")：

> boolean属性的存在表示取值为true，不存在则表示取值为false。

	<input type="text" disabled>
	
	<input type="checkbox" value="1" checked>
	
	<select>
	    <option value="1" selected>1</option>
	</select>

### 2.9 JS生成标签

在JS文件中生成标签让内容变得更难查找，更难编辑，性能更差。应该尽量避免这种情况的出现。

### 2.10 减少标签数量

在编写HTML代码时，需要尽量避免多余的父节点；

很多时候，需要通过迭代和重构来使HTML变得更少。

	<!-- Not well -->
	<span class="avatar">
	    <img src="...">
	</span>
	
	<!-- Better -->
	<img class="avatar" src="...">

### 2.11 实用高于完美

尽量遵循HTML标准和语义，但是不应该以浪费实用性作为代价；

任何时候都要用尽量小的复杂度和尽量少的标签来解决问题。


----------

<h2 id='3'> 3 CSS, SCSS </h2>

### 3.1 缩进

使用soft tab（4个空格）。

	.element {
	    position: absolute;
	    top: 10px;
	    left: 10px;
	
	    border-radius: 10px;
	    width: 50px;
	    height: 50px;
	}

### 3.2 分号

每个属性声明末尾都要加分号。

	.element {
	    width: 20px;
	    height: 20px;
	    background-color: red;
	}

### 3.3 空格

以下几种情况不需要空格：

- 属性名后
- 多个规则的分隔符','前
- !important '!'后
- 属性值中'('后和')'前
- 行末不要有多余的空格

以下几种情况需要空格：

- 属性值前
- 选择器'>', '+', '~'前后
- '{'前
- !important '!'前
- @else 前后
- 属性值中的','后
- 注释'/'后和'/'前

		/* not good */
		.element {
		    color :red! important;
		    background-color: rgba(0,0,0,.5);
		}
		
		/* good */
		.element {
		    color: red !important;
		    background-color: rgba(0, 0, 0, .5);
		}
		
		/* not good */
		.element ,
		.dialog{
		    ...
		}
		
		/* good */
		.element,
		.dialog {
		
		}
		
		/* not good */
		.element>.dialog{
		    ...
		}
		
		/* good */
		.element > .dialog{
		    ...
		}
		
		/* not good */
		.element{
		    ...
		}
		
		/* good */
		.element {
		    ...
		}
		
		/* not good */
		@if{
		    ...
		}@else{
		    ...
		}
		
		/* good */
		@if {
		    ...
		} @else {
		    ...
		}


### 3.4 空行

以下几种情况需要空行：

- 文件最后保留一个空行
- '}'后最好跟一个空行，包括scss中嵌套的规则
- 属性之间需要适当的空行，具体见属性声明顺序

		/* not good */
		.element {
		    ...
		}
		.dialog {
		    color: red;
		    &:after {
		        ...
		    }
		}
		
		/* good */
		.element {
		    ...
		}
		
		.dialog {
		    color: red;
		
		    &:after {
		        ...
		    }
		}

### 3.5 换行

以下几种情况不需要换行：

- '{'前

以下几种情况需要换行：

- '{'后和'}'前
- 每个属性独占一行
- 多个规则的分隔符','后

		/* not good */
		.element
		{color: red; background-color: black;}
		
		/* good */
		.element {
		    color: red;
		    background-color: black;
		}
		
		/* not good */
		.element, .dialog {
		    ...
		}
		
		/* good */
		.element,
		.dialog {
		    ...
		}

### 3.6 注释

注释统一用'/* */'（scss中也不要用'//'），具体参照右边的写法；

缩进与下一行代码保持一致；

可位于一个代码行的末尾，与代码间隔一个空格。

		/* Modal header */
		.modal-header {
		    ...
		}
		
		/*
		 * Modal header
		 */
		.modal-header {
		    ...
		}
		
		.modal-header {
		    /* 50px */
		    width: 50px;
		
		    color: red; /* color red */
		}


### 3.7 引号

最外层统一使用双引号；

url的内容要用引号；

属性选择器中的属性值需要引号。

		.element:after {
		    content: "";
		    background-image: url("logo.png");
		}
		
		li[data-type="single"] {
		    ...
		}

### 3.8 命名

- 类名使用小写字母，以中划线分隔
- id采用驼峰式命名
- scss中的变量、函数、混合、placeholder采用驼峰式命名

		/* class */
		.element-content {
		    ...
		}
		
		/* id */
		#myDialog {
		    ...
		}
		
		/* 变量 */
		$colorBlack: #000;
		
		/* 函数 */
		@function pxToRem($px) {
		    ...
		}
		
		/* 混合 */
		@mixin centerBlock {
		    ...
		}
		
		/* placeholder */
		%myDialog {
		    ...
		}

### 3.9 属性声明顺序

相关的属性声明按右边的顺序做分组处理，组之间需要有一个空行。

		.declaration-order {
		    display: block;
		    float: right;
		
		    position: absolute;
		    top: 0;
		    right: 0;
		    bottom: 0;
		    left: 0;
		    z-index: 100;
		
		    border: 1px solid #e5e5e5;
		    border-radius: 3px;
		    width: 100px;
		    height: 100px;
		
		    font: normal 13px "Helvetica Neue", sans-serif;
		    line-height: 1.5;
		    text-align: center;
		
		    color: #333;
		    background-color: #f5f5f5;
		
		    opacity: 1;
		}
		// 下面是推荐的属性的顺序
		[
		    [
		        "display",
		        "visibility",
		        "float",
		        "clear",
		        "overflow",
		        "overflow-x",
		        "overflow-y",
		        "clip",
		        "zoom"
		    ],
		    [
		        "table-layout",
		        "empty-cells",
		        "caption-side",
		        "border-spacing",
		        "border-collapse",
		        "list-style",
		        "list-style-position",
		        "list-style-type",
		        "list-style-image"
		    ],
		    [
		        "-webkit-box-orient",
		        "-webkit-box-direction",
		        "-webkit-box-decoration-break",
		        "-webkit-box-pack",
		        "-webkit-box-align",
		        "-webkit-box-flex"
		    ],
		    [
		        "position",
		        "top",
		        "right",
		        "bottom",
		        "left",
		        "z-index"
		    ],
		    [
		        "margin",
		        "margin-top",
		        "margin-right",
		        "margin-bottom",
		        "margin-left",
		        "-webkit-box-sizing",
		        "-moz-box-sizing",
		        "box-sizing",
		        "border",
		        "border-width",
		        "border-style",
		        "border-color",
		        "border-top",
		        "border-top-width",
		        "border-top-style",
		        "border-top-color",
		        "border-right",
		        "border-right-width",
		        "border-right-style",
		        "border-right-color",
		        "border-bottom",
		        "border-bottom-width",
		        "border-bottom-style",
		        "border-bottom-color",
		        "border-left",
		        "border-left-width",
		        "border-left-style",
		        "border-left-color",
		        "-webkit-border-radius",
		        "-moz-border-radius",
		        "border-radius",
		        "-webkit-border-top-left-radius",
		        "-moz-border-radius-topleft",
		        "border-top-left-radius",
		        "-webkit-border-top-right-radius",
		        "-moz-border-radius-topright",
		        "border-top-right-radius",
		        "-webkit-border-bottom-right-radius",
		        "-moz-border-radius-bottomright",
		        "border-bottom-right-radius",
		        "-webkit-border-bottom-left-radius",
		        "-moz-border-radius-bottomleft",
		        "border-bottom-left-radius",
		        "-webkit-border-image",
		        "-moz-border-image",
		        "-o-border-image",
		        "border-image",
		        "-webkit-border-image-source",
		        "-moz-border-image-source",
		        "-o-border-image-source",
		        "border-image-source",
		        "-webkit-border-image-slice",
		        "-moz-border-image-slice",
		        "-o-border-image-slice",
		        "border-image-slice",
		        "-webkit-border-image-width",
		        "-moz-border-image-width",
		        "-o-border-image-width",
		        "border-image-width",
		        "-webkit-border-image-outset",
		        "-moz-border-image-outset",
		        "-o-border-image-outset",
		        "border-image-outset",
		        "-webkit-border-image-repeat",
		        "-moz-border-image-repeat",
		        "-o-border-image-repeat",
		        "border-image-repeat",
		        "padding",
		        "padding-top",
		        "padding-right",
		        "padding-bottom",
		        "padding-left",
		        "width",
		        "min-width",
		        "max-width",
		        "height",
		        "min-height",
		        "max-height"
		    ],
		    [
		        "font",
		        "font-family",
		        "font-size",
		        "font-weight",
		        "font-style",
		        "font-variant",
		        "font-size-adjust",
		        "font-stretch",
		        "font-effect",
		        "font-emphasize",
		        "font-emphasize-position",
		        "font-emphasize-style",
		        "font-smooth",
		        "line-height",
		        "text-align",
		        "-webkit-text-align-last",
		        "-moz-text-align-last",
		        "-ms-text-align-last",
		        "text-align-last",
		        "vertical-align",
		        "white-space",
		        "text-decoration",
		        "text-emphasis",
		        "text-emphasis-color",
		        "text-emphasis-style",
		        "text-emphasis-position",
		        "text-indent",
		        "-ms-text-justify",
		        "text-justify",
		        "letter-spacing",
		        "word-spacing",
		        "-ms-writing-mode",
		        "text-outline",
		        "text-transform",
		        "text-wrap",
		        "-ms-text-overflow",
		        "text-overflow",
		        "text-overflow-ellipsis",
		        "text-overflow-mode",
		        "-ms-word-wrap",
		        "word-wrap",
		        "-ms-word-break",
		        "word-break"
		    ],
		    [
		        "color",
		        "background",
		        "filter:progid:DXImageTransform.Microsoft.AlphaImageLoader",
		        "background-color",
		        "background-image",
		        "background-repeat",
		        "background-attachment",
		        "background-position",
		        "-ms-background-position-x",
		        "background-position-x",
		        "-ms-background-position-y",
		        "background-position-y",
		        "-webkit-background-clip",
		        "-moz-background-clip",
		        "background-clip",
		        "background-origin",
		        "-webkit-background-size",
		        "-moz-background-size",
		        "-o-background-size",
		        "background-size"
		    ],
		    [
		        "outline",
		        "outline-width",
		        "outline-style",
		        "outline-color",
		        "outline-offset",
		        "opacity",
		        "filter:progid:DXImageTransform.Microsoft.Alpha(Opacity",
		        "-ms-filter:\\'progid:DXImageTransform.Microsoft.Alpha",
		        "-ms-interpolation-mode",
		        "-webkit-box-shadow",
		        "-moz-box-shadow",
		        "box-shadow",
		        "filter:progid:DXImageTransform.Microsoft.gradient",
		        "-ms-filter:\\'progid:DXImageTransform.Microsoft.gradient",
		        "text-shadow"
		    ],
		    [
		        "-webkit-transition",
		        "-moz-transition",
		        "-ms-transition",
		        "-o-transition",
		        "transition",
		        "-webkit-transition-delay",
		        "-moz-transition-delay",
		        "-ms-transition-delay",
		        "-o-transition-delay",
		        "transition-delay",
		        "-webkit-transition-timing-function",
		        "-moz-transition-timing-function",
		        "-ms-transition-timing-function",
		        "-o-transition-timing-function",
		        "transition-timing-function",
		        "-webkit-transition-duration",
		        "-moz-transition-duration",
		        "-ms-transition-duration",
		        "-o-transition-duration",
		        "transition-duration",
		        "-webkit-transition-property",
		        "-moz-transition-property",
		        "-ms-transition-property",
		        "-o-transition-property",
		        "transition-property",
		        "-webkit-transform",
		        "-moz-transform",
		        "-ms-transform",
		        "-o-transform",
		        "transform",
		        "-webkit-transform-origin",
		        "-moz-transform-origin",
		        "-ms-transform-origin",
		        "-o-transform-origin",
		        "transform-origin",
		        "-webkit-animation",
		        "-moz-animation",
		        "-ms-animation",
		        "-o-animation",
		        "animation",
		        "-webkit-animation-name",
		        "-moz-animation-name",
		        "-ms-animation-name",
		        "-o-animation-name",
		        "animation-name",
		        "-webkit-animation-duration",
		        "-moz-animation-duration",
		        "-ms-animation-duration",
		        "-o-animation-duration",
		        "animation-duration",
		        "-webkit-animation-play-state",
		        "-moz-animation-play-state",
		        "-ms-animation-play-state",
		        "-o-animation-play-state",
		        "animation-play-state",
		        "-webkit-animation-timing-function",
		        "-moz-animation-timing-function",
		        "-ms-animation-timing-function",
		        "-o-animation-timing-function",
		        "animation-timing-function",
		        "-webkit-animation-delay",
		        "-moz-animation-delay",
		        "-ms-animation-delay",
		        "-o-animation-delay",
		        "animation-delay",
		        "-webkit-animation-iteration-count",
		        "-moz-animation-iteration-count",
		        "-ms-animation-iteration-count",
		        "-o-animation-iteration-count",
		        "animation-iteration-count",
		        "-webkit-animation-direction",
		        "-moz-animation-direction",
		        "-ms-animation-direction",
		        "-o-animation-direction",
		        "animation-direction"
		    ],
		    [
		        "content",
		        "quotes",
		        "counter-reset",
		        "counter-increment",
		        "resize",
		        "cursor",
		        "-webkit-user-select",
		        "-moz-user-select",
		        "-ms-user-select",
		        "user-select",
		        "nav-index",
		        "nav-up",
		        "nav-right",
		        "nav-down",
		        "nav-left",
		        "-moz-tab-size",
		        "-o-tab-size",
		        "tab-size",
		        "-webkit-hyphens",
		        "-moz-hyphens",
		        "hyphens",
		        "pointer-events"
		    ]
		]

### 3.10 颜色

颜色16进制用小写字母；

颜色16进制尽量用简写。

		/* not good */
		.element {
		    color: #ABCDEF;
		    background-color: #001122;
		}
		
		/* good */
		.element {
		    color: #abcdef;
		    background-color: #012;
		}

### 3.11 属性简写

属性简写需要你非常清楚属性值的正确顺序，而且在大多数情况下并不需要设置属性简写中包含的所有值，所以建议尽量分开声明会更加清晰；

margin 和 padding 相反，需要使用简写；
常见的属性简写包括：

- font
- background
- transition
- animation

		/* not good */
		.element {
		    transition: opacity 1s linear 2s;
		}
		
		/* good */
		.element {
		    transition-delay: 2s;
		    transition-timing-function: linear;
		    transition-duration: 1s;
		    transition-property: opacity;
		}

### 3.12 媒体查询

尽量将媒体查询的规则靠近与他们相关的规则，不要将他们一起放到一个独立的样式文件中，或者丢在文档的最底部，这样做只会让大家以后更容易忘记他们。

.element {
    ...
}

.element-avatar{
    ...
}

@media (min-width: 480px) {
    .element {
        ...
    }

    .element-avatar {
        ...
    }
}

### 3.13 SCSS相关

提交的代码中不要有 @debug；
声明顺序：

- @extend
- 不包含 @content 的 @include
- 包含 @content 的 @include
- 自身属性
- 嵌套规则

@import 引入的文件不需要开头的'_'和结尾的'.scss'；
嵌套最多不能超过5层；

@extend 中使用placeholder选择器；
去掉不必要的父级引用符号'&'。

		/* not good */
		@import "_dialog.scss";
		
		/* good */
		@import "dialog";
		
		/* not good */
		.fatal {
		    @extend .error;
		}
		
		/* good */
		.fatal {
		    @extend %error;
		}
		
		/* not good */
		.element {
		    & > .dialog {
		        ...
		    }
		}
		
		/* good */
		.element {
		    > .dialog {
		        ...
		    }
		}


### 3.14 杂项

不允许有空的规则；

元素选择器用小写字母；

去掉小数点前面的0；

去掉数字中不必要的小数点和末尾的0；

属性值'0'后面不要加单位；

同个属性不同前缀的写法需要在垂直方向保持对齐，具体参照右边的写法；

无前缀的标准属性应该写在有前缀的属性后面；

不要在同个规则里出现重复的属性，如果重复的属性是连续的则没关系；

不要在一个文件里出现两个相同的规则；

用 border: 0; 代替 border: none;；

选择器不要超过4层（在scss中如果超过4层应该考虑用嵌套的方式来写）；

发布的代码中不要有 @import；

尽量少用'*'选择器。

		/* not good */
		.element {
		}
		
		/* not good */
		LI {
		    ...
		}
		
		/* good */
		li {
		    ...
		}
		
		/* not good */
		.element {
		    color: rgba(0, 0, 0, 0.5);
		}
		
		/* good */
		.element {
		    color: rgba(0, 0, 0, .5);
		}
		
		/* not good */
		.element {
		    width: 50.0px;
		}
		
		/* good */
		.element {
		    width: 50px;
		}
		
		/* not good */
		.element {
		    width: 0px;
		}
		
		/* good */
		.element {
		    width: 0;
		}
		
		/* not good */
		.element {
		    border-radius: 3px;
		    -webkit-border-radius: 3px;
		    -moz-border-radius: 3px;
		
		    background: linear-gradient(to bottom, #fff 0, #eee 100%);
		    background: -webkit-linear-gradient(top, #fff 0, #eee 100%);
		    background: -moz-linear-gradient(top, #fff 0, #eee 100%);
		}
		
		/* good */
		.element {
		    -webkit-border-radius: 3px;
		       -moz-border-radius: 3px;
		            border-radius: 3px;
		
		    background: -webkit-linear-gradient(top, #fff 0, #eee 100%);
		    background:    -moz-linear-gradient(top, #fff 0, #eee 100%);
		    background:         linear-gradient(to bottom, #fff 0, #eee 100%);
		}
		
		/* not good */
		.element {
		    color: rgb(0, 0, 0);
		    width: 50px;
		    color: rgba(0, 0, 0, .5);
		}
		
		/* good */
		.element {
		    color: rgb(0, 0, 0);
		    color: rgba(0, 0, 0, .5);
		}


----------

<h2 id='4'> 4 JavaScript </h2>

### 4.1 缩进

使用soft tab（4个空格）。

		var x = 1,
		    y = 1;
		
		if (x < y) {
		    x += 10;
		} else {
		    x += 1;
		}

### 4.2 单行长度

不要超过80，但如果编辑器开启word wrap可以不考虑单行长度。

### 4.3 分号

以下几种情况后需加分号：

- 变量声明
- 表达式
- return
- throw
- break
- continue
- do-while

		/* var declaration */
		var x = 1;
		
		/* expression statement */
		x++;
		
		/* do-while */
		do {
		    x++;
		} while (x < 10);

### 4.4 空格

以下几种情况不需要空格：

- 对象的属性名后
- 前缀一元运算符后
- 后缀一元运算符前
- 函数调用括号前
- 无论是函数声明还是函数表达式，'('前不要空格
- 数组的'['后和']'前
- 对象的'{'后和'}'前
- 运算符'('后和')'前

以下几种情况需要空格：

- 二元运算符前后
- 三元运算符'?:'前后
- 代码块'{'前
- 下列关键字前：else, while, catch, finally
- 下列关键字后：if, else, for, while, do, switch, case, try,catch, finally, with, return, typeof
- 单行注释'//'后（若单行注释和代码同行，则'//'前也需要），多行注释'*'后
- 对象的属性值前
- for循环，分号后留有一个空格，前置条件如果有多个，逗号后留一个空格
- 无论是函数声明还是函数表达式，'{'前一定要有空格
- 函数的参数之间

		// not good
		var a = {
		    b :1
		};
		
		// good
		var a = {
		    b: 1
		};
		
		// not good
		++ x;
		y ++;
		z = x?1:2;
		
		// good
		++x;
		y++;
		z = x ? 1 : 2;
		
		// not good
		var a = [ 1, 2 ];
		
		// good
		var a = [1, 2];
		
		// not good
		var a = ( 1+2 )*3;
		
		// good
		var a = (1 + 2) * 3;
		
		// no space before '(', one space before '{', one space between function parameters
		var doSomething = function(a, b, c) {
		    // do something
		};
		
		// no space before '('
		doSomething(item);
		
		// not good
		for(i=0;i<6;i++){
		    x++;
		}
		
		// good
		for (i = 0; i < 6; i++) {
		    x++;
		}

### 4.5 空行

以下几种情况需要空行：

- 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
- 注释前（当注释在代码块的第一行时，则无需空行）
- 代码块后（在函数调用、数组、对象中则无需空行）
- 文件最后保留一个空行

		// need blank line after variable declaration
		var x = 1;
		
		// not need blank line when variable declaration is last expression in the current block
		if (x >= 1) {
		    var y = x + 1;
		}
		
		var a = 2;
		
		// need blank line before line comment
		a++;
		
		function b() {
		    // not need blank line when comment is first line of block
		    return a;
		}
		
		// need blank line after blocks
		for (var i = 0; i < 2; i++) {
		    if (true) {
		        return false;
		    }
		
		    continue;
		}
		
		var obj = {
		    foo: function() {
		        return 1;
		    },
		
		    bar: function() {
		        return 2;
		    }
		};
		
		// not need blank line when in argument list, array, object
		func(
		    2,
		    function() {
		        a++;
		    },
		    3
		);
		
		var foo = [
		    2,
		    function() {
		        a++;
		    },
		    3
		];
		
		var foo = {
		    a: 2,
		    b: function() {
		        a++;
		    },
		    c: 3
		};

### 4.6 换行

换行的地方，行末必须有','或者运算符；

以下几种情况不需要换行：

- 下列关键字后：else, catch, finally
- 代码块'{'前

以下几种情况需要换行：

- 代码块'{'后和'}'前
- 变量赋值后

		// not good
		var a = {
		    b: 1
		    , c: 2
		};
		
		x = y
		    ? 1 : 2;
		
		// good
		var a = {
		    b: 1,
		    c: 2
		};
		
		x = y ? 1 : 2;
		x = y ?
		    1 : 2;
		
		// no need line break with 'else', 'catch', 'finally'
		if (condition) {
		    ...
		} else {
		    ...
		}
		
		try {
		    ...
		} catch (e) {
		    ...
		} finally {
		    ...
		}
		
		// not good
		function test()
		{
		    ...
		}
		
		// good
		function test() {
		    ...
		}
		
		// not good
		var a, foo = 7, b,
		    c, bar = 8;
		
		// good
		var a,
		    foo = 7,
		    b, c, bar = 8;

### 4.7 单行注释

双斜线后，必须跟一个空格；

缩进与下一行代码保持一致；

可位于一个代码行的末尾，与代码间隔一个空格。

		if (condition) {
		    // if you made it here, then all security checks passed
		    allowed();
		}
		
		var zhangsan = 'zhangsan'; // one space after code

### 4.8 多行注释

最少三行, '*'后跟一个空格，具体参照右边的写法；

建议在以下情况下使用：

- 难于理解的代码段
- 可能存在错误的代码段
- 浏览器特殊的HACK代码
- 业务逻辑强相关的代码

		/*
		 * one space after '*'
		 */
		var x = 1;

### 4.9 文档注释

各类标签@param, @method等请参考[usejsdoc](http://usejsdoc.org/ "usejsdoc")和[JSDoc Guide](http://yuri4ever.github.io/jsdoc/ "JSDoc Guide")；

建议在以下情况下使用：

- 所有常量
- 所有函数
- 所有类

		/**
		 * @func
		 * @desc 一个带参数的函数
		 * @param {string} a - 参数a
		 * @param {number} b=1 - 参数b默认值为1
		 * @param {string} c=1 - 参数c有两种支持的取值</br>1—表示x</br>2—表示xx
		 * @param {object} d - 参数d为一个对象
		 * @param {string} d.e - 参数d的e属性
		 * @param {string} d.f - 参数d的f属性
		 * @param {object[]} g - 参数g为一个对象数组
		 * @param {string} g.h - 参数g数组中一项的h属性
		 * @param {string} g.i - 参数g数组中一项的i属性
		 * @param {string} [j] - 参数j是一个可选参数
		 */
		function foo(a, b, c, d, g, j) {
		    ...
		}


**顶层/文件注释**

顶层注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西. 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息. 如下:

	// Copyright 2018 PAX Inc. All Rights Reserved.
	
	/**
	 * @fileoverview Description of file, its uses and information
	 * about its dependencies.
	 * @author cqzongjian@google.com (Firstname Lastname)
	 */

**类注释**

每个类的定义都要附带一份注释, 描述类的功能和用法. 也需要说明构造器参数. 如果该类继承自其它类, 应该使用 @extends 标记. 如果该类是对接口的实现, 应该使用 @implements 标记。

	/**
	 * Class making something fun and easy.
	 * @param {string} arg1 An argument that makes this more interesting.
	 * @param {Array.<number>} arg2 List of numbers to be processed.
	 * @constructor
	 * @extends {goog.Disposable}
	 */
	project.MyClass = function(arg1, arg2) {
	  // ...
	};
	goog.inherits(project.MyClass, goog.Disposable);

**方法与函数的注释**

提供参数的说明. 使用完整的句子, 并用第三人称来书写方法说明。

	/**
	 * Converts text to some completely different text.
	 * @param {string} arg1 An argument that makes this more interesting.
	 * @return {string} Some return value.
	 */
	project.MyClass.prototype.someMethod = function(arg1) {
	  // ...
	};
	
	/**
	 * Operates on an instance of MyClass and returns something.
	 * @param {project.MyClass} obj Instance of MyClass which leads to a long
	 *     comment that needs to be wrapped to two lines.
	 * @return {boolean} Whether something occured.
	 */
	function PR_someMethod(obj) {
	  // ...
	}

对于一些简单的, 不带参数的 getters, 说明可以忽略。

	/**
	 * @return {Element} The element for the component.
	 */
	goog.ui.Component.prototype.getElement = function() {
	  return this.element_;
	};

**属性注释**

也需要对属性进行注释。

	/**
	 * Maximum number of things per pane.
	 * @type {number}
	 */
	project.MyClass.prototype.someProperty = 4;

**类型转换的注释**

有时, 类型检查不能很准确地推断出表达式的类型, 所以应该给它添加类型标记注释来明确之, 并且必须在表达式和类型标签外面包裹括号。

	/** @type {number} */ (x)
	(/** @type {number} */ x)



### 4.10 引号

单引号 (') 优于双引号 ("). 当你创建一个包含 HTML 代码的字符串时就知道它的好处了。
最外层统一使用单引号。

		// not good
		var x = "test";
		
		// good
		var y = 'foo',
		    z = '<div id="test"></div>';

### 4.11 变量命名

- 标准变量采用驼峰式命名（除了对象的属性外，主要是考虑到cgi返回的数据）
- 'ID'在变量名中全大写
- 'URL'在变量名中全大写
- 'Android'在变量名中大写第一个字母
- 'iOS'在变量名中小写第一个，大写后两个字母
- 常量全大写，用下划线连接
- 构造函数，大写第一个字母
- jquery对象必须以'$'开头命名
		
		var thisIsMyName;
		
		var goodID;
		
		var reportURL;
		
		var AndroidVersion;
		
		var iOSVersion;
		
		var MAX_COUNT = 10;
		
		function Person(name) {
		    this.name = name;
		}
		
		// not good
		var body = $('body');
		
		// good
		var $body = $('body');

**属性和方法**

- 文件或类中的 私有 属性, 变量和方法名应该以下划线 "_" 开头.
- 保护 属性, 变量和方法名不需要下划线开头, 和公共变量名一样.

**方法和函数参数**

可选参数以 `opt_` 开头.

函数的参数个数不固定时, 应该添加最后一个参数 `var_args` 为参数的个数. 你也可以不设置 `var_args` 而取代使用 `arguments`.

可选和可变参数应该在 `@param` 标记中说明清楚. 虽然这两个规定对编译器没有任何影响, 但还是请尽量遵守

**Getters 和 Setters**

Getters 和 setters 并不是必要的. 但只要使用它们了, 就请将 getters 命名成 `getFoo()` 形式, 将 setters 命名成 `setFoo(value)` 形式. (对于布尔类型的 getters, 使用 `isFoo()` 也可.)

### 4.12 变量声明

一个函数作用域中所有的变量声明尽量提到函数首部，用一个var声明，不允许出现两个连续的var声明。

		function doSomethingWithItems(items) {
		    // use one var
		    var value = 10,
		        result = value + 10,
		        i,
		        len;
		
		    for (i = 0, len = items.length; i < len; i++) {
		        result += 10;
		    }
		}

### 4.13 函数

无论是函数声明还是函数表达式，'('前不要空格，但'{'前一定要有空格；

函数调用括号前不需要空格；

立即执行函数外必须包一层括号；

不要给inline function命名；

参数之间用', '分隔，注意逗号后有一个空格。

		// no space before '(', but one space before'{'
		var doSomething = function(item) {
		    // do something
		};
		
		function doSomething(item) {
		    // do something
		}
		
		// not good
		doSomething (item);
		
		// good
		doSomething(item);
		
		// requires parentheses around immediately invoked function expressions
		(function() {
		    return 1;
		})();
		
		// not good
		[1, 2].forEach(function x() {
		    ...
		});
		
		// good
		[1, 2].forEach(function() {
		    ...
		});
		
		// not good
		var a = [1, 2, function a() {
		    ...
		}];
		
		// good
		var a = [1, 2, function() {
		    ...
		}];
		
		// use ', ' between function parameters
		var doSomething = function(a, b, c) {
		    // do something
		};

### 4.14 数组、对象

对象属性名不需要加引号；

对象以缩进的形式书写，不要写在一行；

数组、对象最后不要有逗号。

		// not good
		var a = {
		    'b': 1
		};
		
		var a = {b: 1};
		
		var a = {
		    b: 1,
		    c: 2,
		};
		
		// good
		var a = {
		    b: 1,
		    c: 2
		};

### 4.15 括号

不要滥用括号, 只在必要的时候使用它。

下列关键字后必须有大括号（即使代码块的内容只有一行）：

`if, else,for, while, do, switch, try, catch, finally, with`。

		// not good
		if (condition)
		    doSomething();
		
		// good
		if (condition) {
		    doSomething();
		}

对于一元操作符(如delete, typeof 和 void ), 或是在某些关键词(如 return, throw, case, new )之后, 不要使用括号。

### 4.16 null

适用场景：

- 初始化一个将来可能被赋值为对象的变量
- 与已经初始化的变量做比较
- 作为一个参数为对象的函数的调用传参
- 作为一个返回对象的函数的返回值

不适用场景：

- 不要用null来判断函数调用时有无传参
- 不要与未初始化的变量做比较

		// not good
		function test(a, b) {
		    if (b === null) {
		        // not mean b is not supply
		        ...
		    }
		}
		
		var a;
		
		if (a === null) {
		    ...
		}
		
		// good
		var a = null;
		
		if (a === null) {
		    ...
		}

### 4.17 undefined

永远不要直接使用undefined进行变量判断；

使用typeof和字符串'undefined'对变量进行判断。

		// not good
		if (person === undefined) {
		    ...
		}
		
		// good
		if (typeof person === 'undefined') {
		    ...
		}

### 4.18 jshint

- 用'===', '!=='代替'==', '!='；
- `for-in`里一定要有`hasOwnProperty`的判断；
- 不要在内置对象的原型上添加方法，如`Array`, `Date`；
- 不要在内层作用域的代码里声明了变量，之后却访问到了外层作用域的同名变量；
- 变量不要先使用后声明；
- 不要在一句代码中单单使用构造函数，记得将其赋值给某个变量；
- 不要在同个作用域下声明同名变量；
- 不要在一些不需要的地方加括号，例：`delete(a.b)`；
- 不要使用未声明的变量（全局变量需要加到`.jshintrc`文件的`globals`属性里面）；
- 不要声明了变量却不使用；
- 不要在应该做比较的地方做赋值；
- `debugger`不要出现在提交的代码里；
- 数组中不要存在空元素；
- 不要在循环内部声明函数；
- 不要像这样使用构造函数，例：`new function () { ... },` `new Object`；

		// not good
		if (a == 1) {
		    a++;
		}
		
		// good
		if (a === 1) {
		    a++;
		}
		
		// good
		for (key in obj) {
		    if (obj.hasOwnProperty(key)) {
		        // be sure that obj[key] belongs to the object and was not inherited
		        console.log(obj[key]);
		    }
		}
		
		// not good
		Array.prototype.count = function(value) {
		    return 4;
		};
		
		// not good
		var x = 1;
		
		function test() {
		    if (true) {
		        var x = 0;
		    }
		
		    x += 1;
		}
		
		// not good
		function test() {
		    console.log(x);
		
		    var x = 1;
		}
		
		// not good
		new Person();
		
		// good
		var person = new Person();
		
		// not good
		delete(obj.attr);
		
		// good
		delete obj.attr;
		
		// not good
		if (a = 10) {
		    a++;
		}
		
		// not good
		var a = [1, , , 2, 3];
		
		// not good
		var nums = [];
		
		for (var i = 0; i < 10; i++) {
		    (function(i) {
		        nums[i] = function(j) {
		            return i + j;
		        };
		    }(i));
		}
		
		// not good
		var singleton = new function() {
		    var privateVar;
		
		    this.publicMethod = function() {
		        privateVar = 1;
		    };
		
		    this.publicMethod2 = function() {
		        privateVar = 2;
		    };
		};


### 4.19 块内函数声明

不要在块内声明一个函数。

不要写成:

	if (x) {
	  function foo() {}
	}

虽然很多 JS 引擎都支持块内声明函数, 但它不属于 ECMAScript 规范 (见 [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm "ECMA-262"), 第13和14条). 各个浏览器糟糕的实现相互不兼容, 有些也与未来 ECMAScript 草案相违背. ECMAScript 只允许在脚本的根语句或函数中声明函数. 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

	if (x) {
	  var foo = function() {}
	}


### 4.20 关联数组

永远不要使用 Array 作为 map/hash/associative 数组。

数组中不允许使用非整型作为索引值, 所以也就不允许用关联数组. 而取代它使用 Object 来表示 map/hash 对象. Array 仅仅是扩展自 Object (类似于其他 JS 中的对象, 就像 Date, RegExp 和 String)一样来使用。

### 4.21 多行字符串

不要使用。

不要这样写长字符串:

	var myString = 'A rather long string of English text, an error message \
	                actually that just keeps going and going -- an error \
	                message to make the Energizer bunny blush (right through \
	                those Schwarzenegger shades)! Where was I? Oh yes, \
	                you\'ve got an error and all the extraneous whitespace is \
	                just gravy.  Have a nice day.';

在编译时, 不能忽略行起始位置的空白字符; "\" 后的空白字符会产生奇怪的错误; 虽然大多数脚本引擎支持这种写法, 但它不是 ECMAScript 的标准规范。

### 4.22 Array 和 Object 直接量

使用 Array 和 Object 语法, 而不使用 Array 和 Object 构造器.

使用 Array 构造器很容易因为传参不恰当导致错误.

	// Length is 3.
	var a1 = new Array(x1, x2, x3);
	
	// Length is 2.
	var a2 = new Array(x1, x2);
	
	// If x1 is a number and it is a natural number the length will be x1.
	// If x1 is a number but not a natural number this will throw an exception.
	// Otherwise the array will have one element with x1 as its value.
	var a3 = new Array(x1);
	
	// Length is 0.
	var a4 = new Array();

如果传入一个参数而不是2个参数, 数组的长度很有可能就不是你期望的数值了.

为了避免这些歧义, 我们应该使用更易读的直接量来声明.

	var a = [x1, x2, x3];
	var a2 = [x1, x2];
	var a3 = [x1];
	var a4 = [];

虽然 Object 构造器没有上述类似的问题, 但鉴于可读性和一致性考虑, 最好还是在字面上更清晰地指明.

	var o = new Object();
	
	var o2 = new Object();
	o2.a = 0;
	o2.b = 1;
	o2.c = 2;
	o2['strange key'] = 3;

应该写成:

	var o = {};
	
	var o2 = {
	  a: 0,
	  b: 1,
	  c: 2,
	  'strange key': 3
	};


### 4.23 杂项

不要混用tab和space；

不要在一处使用多个tab或space；

换行符统一用'LF'；

对上下文`this`的引用只能使用'`_this`', '`that`', '`self`'其中一个来命名；

行尾不要有空白字符；

`switch`的`falling through`和`no default`的情况一定要有注释特别说明；

不允许有空的代码块。

		// not good
		var a   = 1;
		
		function Person() {
		    // not good
		    var me = this;
		
		    // good
		    var _this = this;
		
		    // good
		    var that = this;
		
		    // good
		    var self = this;
		}
		
		// good
		switch (condition) {
		    case 1:
		    case 2:
		        ...
		        break;
		    case 3:
		        ...
		    // why fall through
		    case 4
		        ...
		        break;
		    // why no default
		}
		
		// not good with empty block
		if (condition) {
		
		}

### 4.24 Tips and Tricks

JavaScript 小技巧：

**True 和 False 布尔表达式**

下面的布尔表达式都返回 false:

	null
	undefined
	'' 空字符串
	0 数字0

但小心下面的, 可都返回 true:

	'0' 字符串0
	[] 空数组
	{} 空对象

下面段比较糟糕的代码:

	while (x != null) {

你可以直接写成下面的形式(只要你希望 x 不是 0 和空字符串, 和 false):

	while (x) {

如果你想检查字符串是否为 null 或空:

	if (y != null && y != '') {

但这样会更好:

	if (y) {

注意: 还有很多需要注意的地方, 如:

	

	Boolean('0') == true
	'0' != true

	0 != null
	0 == []
	0 == false

	Boolean(null) == false
	null != true
	null != false

	Boolean(undefined) == false
	undefined != true
	undefined != false

	Boolean([]) == true
	[] != true
	[] == false

	Boolean({}) == true
	{} != true
	{} != false

**条件(三元)操作符 (?:)**

三元操作符用于替代下面的代码:

	if (val != 0) {
	  return foo();
	} else {
	  return bar();
	}

你可以写成:

	return val ? foo() : bar();

在生成 HTML 代码时也是很有用的:

	var html = '<input type="checkbox"' +
	    (isChecked ? ' checked' : '') +
	    (isEnabled ? '' : ' disabled') +
	    ' name="foo">';

**&& 和 ||**

二元布尔操作符是可短路的, 只有在必要时才会计算到最后一项.

"||" 被称作为 'default' 操作符, 因为可以这样:

	/** @param {*=} opt_win */
	function foo(opt_win) {
	  var win;
	  if (opt_win) {
	    win = opt_win;
	  } else {
	    win = window;
	  }
	  // ...
	}

你可以使用它来简化上面的代码:

	/** @param {*=} opt_win */
	function foo(opt_win) {
	  var win = opt_win || window;
	  // ...
	}

"&&" 也可简短代码.比如:

	if (node) {
	  if (node.kids) {
	    if (node.kids[index]) {
	      foo(node.kids[index]);
	    }
	  }
	}

你可以像这样来使用:

	if (node && node.kids && node.kids[index]) {
	  foo(node.kids[index]);
	}

或者:

	var kid = node && node.kids && node.kids[index];
	if (kid) {
	  foo(kid);
	}

不过这样就有点儿过头了:

	node && node.kids && node.kids[index] && foo(node.kids[index]);

**使用 join() 来创建字符串**

通常是这样使用的:

	function listHtml(items) {
	  var html = '<div class="foo">';
	  for (var i = 0; i < items.length; ++i) {
	    if (i > 0) {
	      html += ', ';
	    }
	    html += itemHtml(items[i]);
	  }
	  html += '</div>';
	  return html;
	}

但这样在 IE 下非常慢, 可以用下面的方式:

	function listHtml(items) {
	  var html = [];
	  for (var i = 0; i < items.length; ++i) {
	    html[i] = itemHtml(items[i]);
	  }
	  return '<div class="foo">' + html.join(', ') + '</div>';
	}

你也可以是用数组作为字符串构造器, 然后通过 `myArray.join('')` 转换成字符串. 不过由于赋值操作快于数组的 `push()`, 所以尽量使用赋值操作.

**遍历 Node List**

Node lists 是通过给节点迭代器加一个过滤器来实现的. 这表示获取他的属性, 如 length 的时间复杂度为 O(n), 通过 length 来遍历整个列表需要 O(n^2).

	var paragraphs = document.getElementsByTagName('p');
	for (var i = 0; i < paragraphs.length; i++) {
	  doSomething(paragraphs[i]);
	}

这样做会更好:

	var paragraphs = document.getElementsByTagName('p');
	for (var i = 0, paragraph; paragraph = paragraphs[i]; i++) {
	  doSomething(paragraph);
	}

这种方法对所有的 `collections` 和数组(只要数组不包含 `falsy` 值) 都适用.

在上面的例子中, 也可以通过 `firstChild` 和 `nextSibling` 来遍历孩子节点.

	var parentNode = document.getElementById('foo');
	for (var child = parentNode.firstChild; child; child = child.nextSibling) {
	  doSomething(child);
	}


### 4.25 Parting Words

保持一致性。

当你在编辑代码之前, 先花一些时间查看一下现有代码的风格. 如果他们给算术运算符添加了空格, 你也应该添加. 如果他们的注释使用一个个星号盒子, 那么也请你使用这种方式。

代码风格中一个关键点是整理一份常用词汇表, 开发者认同它并且遵循, 这样在代码中就能统一表述。我们在这提出了一些全局上的风格规则, 但也要考虑自身情况形成自己的代码风格. 但如果你添加的代码和现有的代码有很大的区别, 这就让阅读者感到很不和谐. 所以, 避免这种情况的发生。



----------

## 参考资料

1. [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html "Google HTML/CSS Style Guide")
1. [Google JavaScript Style Guide](http://google.github.io/styleguide/javascriptguide.xml "Google JavaScript Style Guide")
1. [Code Guide by @AlloyTeam](http://alloyteam.github.io/CodeGuide/ "Code Guide by @AlloyTeam")