### 1 通用

1.1 文件命名

css文件存放在对应的目录下。

命名遵循首字母小写，驼峰命名法。

```
// good
telSale文件下：
allSensitiveActions.css

// bad
telSale文件下：
AllSensitiveActions.css

// bad
telSale文件下：
all_sensitive_actions.css
```
1.2 移动端目前是以 rem 布局为主，媒体查询为辅。

设计稿的尺寸是以 640 为基准。

1.3 不要轻易改动全站级CSS和通用CSS库，改动后，要经过全面测试。

1.4 注释规范

* 功能模块注释，分模块来注释CSS样式（如：头部、导航、按钮、页脚等等）

### 2、代码风格

2.1 缩进

遵循.eslintrc规则，使用 tab 做为一个缩进层级。

```
#main .u-content-single {
	width: 100px;
	height: 100px;
}
```

2.2 换行

（1）花括号前后、属性与属性值之间执行换行操作。

每行不得超过 120 个字符。

```
#main .u-content-single {
	width: 100px;
	height: 100px;
}
```
（2）单条规则需在一行表示，多条规则以逗号分割，并另起一行

```
#main .u-content,
#main .u-content-edit {
	width: 100px;
	height: 100px;
}
#main .u-content-single {
	width: 100px;
	height: 100px;
}
```

（3）不同模块间增加空行处理

```
#main .u-top {}

#main .u-middle {}
```

2.3 空格

花括号前后、声明之间、属性与属性值之间都需要插入一个空格；

```
#main .u-content-single {
	width: 100px;
}
```

2.4 冒号

属性之间都需要插入一个冒号（ ; ）

```
// good
#main .u-content-single {
	width: 100px;
	height: 100px;
}

// bad
#main .u-content-single {
	width: 100px
	height: 100px
}
```

### 3、选择器

3.1 如无必要，不得为 id、class 选择器添加类型选择器进行限定。
对类型选择器限定在性能维护上，有一定的影响。

```
// good
#error,
.u-danger-message {
    font-color: #c00;
}

// bad
dialog#error,
p.u-danger-message {
    font-color: #c00;
}
```

3.2 选择器的嵌套层级应不大于 3 级，位置靠后的限定条件应尽可能精确。

```
// good
#username input {}
.u-comment .u-avatar {}

// bad
.u-page .u-header .u-login #username input {}
.u-comment div * {}

```

3.3 不能使用 id 选择器编写属性与属性值

```
// good
.u-content-single {
	width: 100px;
}

// bad
#u-content-single {
	width: 100px;
}

```

3.4 >、+、~ 选择器的两边各保留一个空格。

```
// good
main > nav {
    padding: 10px;
}

label + input {
    margin-left: 5px;
}

input:checked ~ button {
    background-color: #69C;
}

// bad
main>nav {
    padding: 10px;
}

label+input {
    margin-left: 5px;
}

input:checked~button {
    background-color: #69C;
}

```

3.5 属性选择器中的值必须用双引号包围。

```
// good
article[character="juliet"] {
    voice-family: "Vivien Leigh", victoria, female;
}

// bad
article[character='juliet'] {
    voice-family: "Vivien Leigh", victoria, female;
}

```


### 4、属性

4.1 属性缩写

在可以使用缩写的情况下，尽量使用属性缩写。

```
// good
.u-post {
    font: 12px/1.5 arial, sans-serif;
}

// bad
.u-post {
    font-family: arial, sans-serif;
    font-size: 12px;
    line-height: 1.5;
}
```

4.2 属性顺序

使用属性顺序的前提，局部的一个小功能，已经不需要按 class 功能划分。

Formatting Model（布局方式、位置） > Box Model（尺寸） > Typographic（文本相关） > Visual（视觉效果） 的顺序书写，以提高代码的可读性。

(可参考 bootstrap)

```
.u-sidebar {
    /* formatting model: positioning schemes / offsets / z-indexes / display / ...  */
    position: absolute;
    top: 50px;
    left: 0;
    overflow-x: hidden;

    /* box model: sizes / margins / paddings / borders / ...  */
    width: 200px;
    padding: 5px;
    border: 1px solid #ddd;

    /* typographic: font / aligns / text styles / ... */
    font-size: 14px;
    line-height: 20px;

    /* visual: colors / shadows / gradients / ... */
    background: #f5f5f5;
    color: #333;
    -webkit-transition: color 1s;
       -moz-transition: color 1s;
            transition: color 1s;
}

```


4.3 !important

尽量不使用 !important 声明。

若要使用可通过行内样式定义，其次为 !important

如果使用避免全局使用


### 5、值与单位

5.1 数值

当数值为 0 - 1 之间的小数时，省略整数部分的 0。

```
panel {
    opacity: .8
}

.u-children { 
	background: rgba(255, 255, 255, .4); 
}
```

5.2 色值

颜色色值尽量使用简写形式的十六进制，且十六进制应该全部小写。

```
// bad
#main .u-content { 
	color: #FFF; 
}

// bad
#main .u-content { 
	color: #ffffff; 
}

// good
#main .u-content { 
	color: #fff; 
}
```

5.3 长度

长度为 0 时须省略单位。 (也只有长度单位可省)

```
// good
body {
    padding: 0 5px;
}

// bad
body {
    padding: 0px 5px;
}
```

### 6、颜色

6.1 RGB颜色值必须使用十六进制形式，不允许使用 rgb()。

颜色信息可以使用 rgba()。使用 rgba() 时每个逗号后必须保留一个空格。

```
// good
.u-success {
    box-shadow: 0 0 2px rgba(0, 128, 0, .3);
    border-color: #008000;
}

// bad
.u-success {
    box-shadow: 0 0 2px rgba(0,128,0,.3);
    border-color: rgb(0, 128, 0);
}
```

6.2 颜色值可以缩写时，必须使用缩写形式。

```
// good
.u-success {
    background-color: #aca;
}

// bad
.u-success {
    background-color: #aaccaa;

```

6.3 颜色值不允许使用命名色值。

```
// good
.u-success {
    color: #90ee90;
}

// bad
.u-success {
    color: lightgreen;
}
```


### 7、组件

7.1 复用样式

* 组件的修饰表示基于原组件的样式在某些特定情况下的变化，命名方式为在前面的基础上加上“ - ”。
* 在使用时必须是以原样式名+修饰样式名的形式出现。

```
// good
.u-btn-active {
	width: 110px;
}

.u-btn-default {
	width: 100px;
}

// bad
#main .u-btn {
	width: 100px;
}


```
7.2 组件

* 除了公共模块，样式选择器起始需加上最外层的 id 用于根选择器

* 子组件是隶属于组件的，像下面的 header 是 #articleBox 的一部分

```
css
// good
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

