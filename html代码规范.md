
### 1、通用

1.1 文档类型

使用 HTML5 的 DOCTYPE 来启用标准模式(大写)。

添加标准模式声明，确保在每个浏览器中拥有一致的表现。

```
<!DOCTYPE html>
```

1.2 CSS和JavaScript引入

（1）引入 CSS 时必须指明 rel="stylesheet"

```
<link rel="stylesheet" src="page.css">
```
（2）在 head 中提前引入页面需要的所有 CSS 资源，避免新加载元素的样式，导致页面闪烁。

（3）JavaScript 应当放在页面末尾，或采用异步加载。

```
<body>
    <!-- a lot of elements -->
    <script src="init.js"></script>
</body>
```

1.3 页面初始化

页面最外层标签，带上一个 id（用于书写样式）和 data-lb-page（用于初始化 js 代码）

```
<div id="main"  data-lb-page="main">
  XXX 具体内容
</div>

```

### 2、命名规范


2.1 文件命名

html文件存放在对应的目录下。

命名遵循首字母小写，驼峰命名法。


```
// good
telSale文件下：
allSensitiveActions.njk

// bad
telSale文件下：
AllSensitiveActions.njk

// bad
telSale文件下：
all_sensitive_actions.njk
```


2.2 id 命名

id 用于标识具体组件。

id 命名规则，首字母小写，采用驼峰命名法。

```
// good
<div id=“camelCase”>
	exmaple
</p>

// bad
<p id=“camel_case”>
	exmaple
</p>
```

2.3 class 样式命名

用于标识高度可复用组件。

(1) 在class选择器中，采用 “u-” 开头，以“ - ”隔开词意。

```
// good
<p class=“u-word-practice-lesson”></p>

// bad
<p id=“u-word-practice-lessonl”></p>

// bad
<p class=“word-practice-lessonl”></p>

// bad
<p class=“u-word_practice_lessonl”></p>

// bad
<p class=“u-wordPracticeLessonl”></p>
```

(2) 组件、可复用的样式，采用分类名式命名。

命名顺序Formatting Model（布局方式、位置） > Box Model（尺寸） > Typographic（文本相关） > Visual（视觉效果） 的顺序书写，以提高代码的可读性。

formatting model: positioning schemes / offsets / z-indexes / display / ...

box model: sizes / margins / paddings / borders / ...

typographic: font / aligns / text styles / ...

visual: colors / shadows / gradients / ...


```
// good
<div class="u-formatting-model u-box-model u-typographic u-visual">
	<button class='u-buttons-wrap'>操作</button>
</div>

// bad
<div class="u-box">
	<button class='u-buttons-wrap'>操作</button>
</div>
```

2.4 class 操作命名

在class选择器中，采用 “j-” 开头，首字母小写，采用驼峰命名法。

```
// good
<p class=“j-unApproveExtOrderForm”></p>

// bad
<p id=“j-unApproveExtOrderForm”></p>

// bad
<p class=“unApproveExtOrderForm”></p>

// bad
<p class=“j-un_approve-ext-order-form”></p>

// bad
<p class=“j-un_approve_ext_order_form”></p>
```

2.5 img类名

	* 背景：以bg作为命名空间，例如：u-bg-body 等；

	* 图标：以ico作为命名空间，例如：u-ico-close 等；

	* LOGO：以logo作为命名空间，例如：u-logo-duowan 等；

	* 内容图像：以img作为命名空间，例如：u-img-userGuide 等；

	* 雪碧图：以sprite作为命名空间，例如：u-sprite-form 等；

2.6 命名长度

在避免冲突并描述清楚的前提下尽可能短。

但不可以自己随意简写，简写的一个重要标准是大家约定且都认识的（或在全局已注释说明）。

```
// good
<p class=“u-word-practice-lesson”></p>

// bad
<p class=“u-wpl”></p>
```
### 3、head

3.1 字符编码

以无 BOM 的 utf-8 编码作为文件格式。

```
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

3.2 IE Edge 模式

优先使用最新版本的IE 和 Chrome 内核

```
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

3.3 title

页面必须包含 title 标签声明标题。

```
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

3.4 viewport

* viewport: 一般指的是浏览器窗口内容区的大小，不包含工具条、选项卡等内容；
* width: 浏览器宽度，输出设备中的页面可见区域宽度；
* device-width: 设备分辨率宽度，输出设备的屏幕可见宽度；
* initial-scale: 初始缩放比例；
* maximum-scale: 最大缩放比例；

为移动端设备优化，设置可见区域的宽度和初始缩放比例。

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

3.5 SEO 优化

```
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <!-- SEO -->
    <title>Style Guide</title>
    <meta name="keywords" content="your keywords">
    <meta name="description" content="your description">
    <meta name="author" content="author,email address">
</head>

```
### 4、标签


4.1 标签使用

标签的使用应该遵循标签的语义。

* p - 段落
* h1,h2,h3,h4,h5,h6 - 层级标题
* strong,em - 强调

    ```
    <html>
      <head>
        <title>朗播网</title>
      </head>
      <body>
        <div class="u-top">
            <h1 class="u-header">朗播网</h1>
            <input type="text" disabled>
        </div>

        <div>
             <img src="images/company-logo.png" alt="Company" title=“朗播网”>
        </div>
      </body>
    </html>
    ```

4.2 标签必须使用小写字母。

```
// good
<h1>Hello word!</h1>

// bad
<H1>Hello word!</H1>
```

4.3 标签闭合

（1）自闭合标签不闭合。

常见无需自闭合标签有input、br、img、hr等。

```
// good
<input name="title" type="text">

// bad
<input name="title" type="text" />
```

（2）闭合标签必须闭合。

```
// good
<ul>
    <li>first</li>
    <li>second</li>
</ul>

// bad
<ul>
    <li>first
    <li>second
</ul>
```
4.4 缩进与换行

遵循.eslintrc规则，使用 tab 做为一个缩进层级。

每行不得超过 120 个字符。

```
<ul>
    <li>first</li>
    <li>second</li>
</ul>
```

### 5、img

5.1 src属性

禁止 img 的 src 取值为空。延迟加载的图片也要增加默认的 src。

src 取值为空，会导致部分浏览器重新加载一次当前页面。

```
// good
<img src=“http://”>

// bad
<img src=“”>
```

5.2 title属性

避免为 img 添加不必要的 title 属性。

多余的 title 影响看图体验，并且增加了页面尺寸。

5.3 alt属性。

为重要图片添加 alt 属性。

```
<img src=“http://” alt="图书logo">

```

5.4 width和height属性

添加 width 和 height 属性，避免加载前后页面抖动。

```
<img src=“http://” alt="图书logo" width=“240px” height=“120px”>

```

5.5 img命名

	* 背景：以bg作为命名空间，例如：bg-body 等；

	* 图标：以ico作为命名空间，例如：ico-close 等；

	* LOGO：以logo作为命名空间，例如：logo-duowan 等；

	* 内容图像：以img作为命名空间，例如：img-userGuide 等；

	* 雪碧图：以sprite作为命名空间，例如：sprite-form 等；


### 6、属性

6.1 标签属性必须使用小写字母。

```
// good
<input data-state=“title” type="text">

// bad
<input data-State=“title” type="text" />
```

6.2 引号

属性的定义，确保全部使用双引号，绝不要使用单引号。

```
// good
<input data-state=“title“ type="text">

// bad
<input data-state=‘title’ type=‘text’ />
```

6.3 布尔型属性

布尔型属性可以在声明时不赋值。

```
<input type="text" disabled >
```

6.4 属性顺序

（1）HTML 属性应当按照以下给出的顺序依次排列，确保代码的易读性。

    * class
    * id, name
    * data-*
    * src, for, type, href, value
    * title, alt
    * role, aria-*

（2）class 用于标识高度可复用组件，因此应该排在首位。id 用于标识具体组件，应当谨慎使用（例如，页面内的书签），因此排在第二位。

```
<a class="..." id="..." data-toggle="modal" href="#">
  Example link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```
（3）页面最外层标签，带上一个 id（用于书写样式）和 data-lb-page（用于初始化 js 代码）

    ```
    <div id="main"  data-lb-page="main">
      XXX 具体内容
    </div>
    ```
### 7、组件

7.1 除了公共模块，样式选择器起始需加上最外层的 id 用于根选择器

class 用于标识高度可复用组件，因此应该排在首位。id 用于标识具体组件，应当谨慎使用（例如，页面内的书签），因此排在第二位。

```
<div class="..." id="..." data-toggle="modal" href="#">
    <input class="form-control" type="text">
    <img src="..." alt="...">
</div>

```

7.2 复用样式

* 组件的修饰表示基于原组件的样式在某些特定情况下的变化，命名方式为在前面的基础上加上“ - ”。
* 在使用时必须是以原样式名+修饰样式名的形式出现。

```
css
.u-btn {
    width: 90px;
}

.u-btn-default {
    color: #000;
}


html
<button class="u-btn u-btn-primary">…</button>

```

7.3 子组件

* 子组件是隶属于组件的，像下面的 header 是 #articleBox 的一部分

```
css
#articleBox .u-tweet-header {
	width: 110px;
}

html
<article class="u-tweet" id=“articleBox”>
  <header class="u-tweet-header">
    <img class="u-tweet-avatar" src="{$src}" alt="{$alt}">
    …
  </header>
</article>

```
