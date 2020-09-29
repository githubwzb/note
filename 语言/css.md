# CSS学习笔记
##简介
CSS 指层叠样式表 (Cascading Style Sheets)。对于一个站点而言，它的每个页面中存在多个组件，其中的部分组件是可以重复使用的。将这种可以重复使用的组件予以统一的一次性定义的方法，就是样式表。使用CSS可以避免我们对重复使用的组件进行重复定义，从而减少工作量。并且以后如果要更改样式，只需要对样式表进行更改就能更改一个站点的所有页面上的对应组件，大大减少了工作量。这就是学习和使用CSS的意义所在。
学习CSS之前，你要掌握HTML与XHTML的相关知识。
##语法
CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。
`selector {declaration1; declaration2; ... declarationN }`
选择器通常是您需要改变样式的 HTML 元素。
每条声明由一个属性和一个值组成。属性（property）是您希望设置的样式属性（style attribute）。每个属性有一个值。属性和值被冒号分开。

`selector {property: value}
下面这行代码的作用是将 h1 元素内的文字颜色定义为红色，同时将字体大小设置为 14 像素。

在这个例子中，h1 是选择器，color 和 font-size 是属性，red 和 14px 是值。

`h1 {color:red; font-size:14px;}`

除了英文单词 red，我们还可以使用十六进制的颜色值 [[ff0000]]：
```css
p { color: [[ff0000]]; }
```
我们还可以通过两种方法使用 RGB 值：
```css
p { color: rgb(255,0,0); }
p { color: rgb(100%,0%,0%); }
```
不要忘记打花括号，以及每个属性所对应的分号。
如果值为若干单词，则要给值加引号：
`p {font-family: "sans serif";} `

如果有多个声明建议采用类似下列代码的方式。
```css
p {
  text-align: center;
  color: black;
  font-family: arial;
}
```
CSS 对大小写不敏感,也就是说，大写字母与小写字母是等价的。但如果涉及到与 HTML 文档一起工作的话，class 和 id 名称对大小写是敏感的。

## 选择器的分组
你可以对选择器进行分组，这样，被分组的选择器就可以分享相同的声明。用逗号将需要分组的选择器分开。在下面的例子中，我们对所有的标题元素进行了分组。所有的标题元素都是绿色的。
```css
h1,h2,h3,h4,h5,h6 {
  color: green;
  }
```

## CSS的继承问题

根据 CSS，子元素从父元素继承属性
```css
body 
{
color: black;
}
```
将使所有的body的子元素继承body的颜色属性：黑色。如果有特殊声明的，不会继承，如
```css
body
{
color:black;
}
p
{
color:white;
}

```
那么，body和它的子元素（除了p）将拥有属性黑色，而p将会是白色。
## CSS 派生选择器
通过依据元素在其位置的上下文关系来定义样式，你可以使标记更加简洁。
```css
li strong{ font-style: italic;font-weight: normal;} 
```
这条CSS语句将使在li元素中的strong元素显示为斜体而不是粗体。而一般的li或strong元素将不受影响。

## id 选择器
id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。
### id 选择器以 "#" 来定义。
下面的两个 id 选择器，第一个可以定义元素的颜色为红色，第二个定义元素的颜色为绿色：
```css
[[red]] {color:red;}
[[green]] {color:green;}
```
下面的 HTML 代码中，id 属性为 red 的 p 元素显示为红色，而 id 属性为 green 的 p 元素显示为绿色。

<p id="red">这个段落是红色。</p>
<p id="green">这个段落是绿色。</p>
注意：id 属性只能在每个 HTML 文档中出现一次

[[id]] 选择器和派生选择器
在现代布局中，id 选择器常常用于建立派生选择器。
```css
[[sidebar]] p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}
```
上面的样式只会应用于出现在 `id` 是 `sidebar` 的元素内的段落。这个元素很可能是 div 或者是表格单元，尽管它也可能是一个表格或者其他块级元素。它甚至可以是一个内联元素，比如 `<em></em>` 或者 `<span></span>`，不过这样的用法是非法的，因为不可以在内联元素 <span> 中嵌入 <p>
###一个选择器多种用法
即使被标注为 sidebar 的元素只能在文档中出现一次，这个 id 选择器作为派生选择器也可以被使用很多次：
```css
[[sidebar]] p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}

[[sidebar]] h2 {
	font-size: 1em;
	font-weight: normal;
	font-style: italic;
	margin: 0;
	line-height: 1.5;
	text-align: right;
	}
```
以上代码就特殊处理了sidebar的p和h2对象。
___
##类选择器

在 CSS 中，类选择器以一个点号显示：
`.center {text-align: center}`

在上面的例子中，所有拥有 center 类的 HTML 元素均为居中。

在下面的 HTML 代码中，h1 和 p 元素都有 center 类。这意味着两者都将遵守 ".center" 选择器中的规则。

<h5 class="center">
This heading will be center-aligned
</h5>
<p class="center">
This paragraph will also be center-aligned.
</p>
注意：类名的第一个字符不能使用数字！它无法在 Mozilla 或 Firefox 中起作用。

和 id 一样，class 也可被用作派生选择器：
```css
.fancy td {
	color: [[f60]];
	background: #666;
	}
```
在上面这个例子中，类名为 fancy 的更大的元素内部的表格单元都会以灰色背景显示橙色文字。（名为 fancy 的更大的元素可能是一个表格或者一个 div）

`<td class="fancy">`
你可以将类 fancy 分配给任何一个表格元素任意多的次数。那些以 fancy 标注的单元格都会是带有灰色背景的橙色。那些没有被分配名为 fancy 的类的单元格不会受这条规则的影响。还有一点值得注意，class 为 fancy 的段落也不会是带有灰色背景的橙色，当然，任何其他被标注为 fancy 的元素也不会受这条规则的影响。这都是由于我们书写这条规则的方式，这个效果被限制于被标注为 fancy 的表格单元（即使用 td 元素来选择 fancy 类）。

[[CSS]] 属性选择器
###属性选择器
下面的例子为带有 title 属性的所有元素设置样式：
```css
[title]
{
color:red;
}
```
###属性和值选择器
下面的例子为 title="W3School" 的所有元素设置样式：
```css
[title=W3School]
{
border:5px solid blue;
}
```
###属性和值选择器 - 多个值
下面的例子为包含指定值的 title 属性的所有元素设置样式。适用于由空格分隔的属性值：

`[title~=hello] { color:red; }`
下面的例子为带有包含指定值的 lang 属性的所有元素设置样式。适用于由连字符分隔的属性值：

`[lang|=en] { color:red; }`
###设置表单的样式
属性选择器在为不带有 class 或 id 的表单设置样式时特别有用：
```css
input[type="text"]
{
  width:150px;
  display:block;
  margin-bottom:10px;
  background-color:yellow;
  font-family: Verdana, Arial;
}

input[type="button"]
{
  width:120px;
  margin-left:35px;
  display:block;
  font-family: Verdana, Arial;
}
```

CSS 选择器参考手册
选择器|	描述
--|--
[attribute]	|用于选取带有指定属性的元素。
[attribute=value]|	用于选取带有指定属性和值的元素。
[attribute~=value]|	用于选取属性值中包含指定词汇的元素。
[attribute|=value]|	用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。
[attribute^=value]	|匹配属性值以指定值开头的每个元素。
[attribute$=value]	|匹配属性值以指定值结尾的每个元素。
[attribute*=value]|	匹配属性值中包含指定值的每个元素。

##如何创建 CSS
###如何插入样式表
当读到一个样式表时，浏览器会根据它来格式化 HTML 文档。插入样式表的方法有三种：

####外部样式表
当样式需要应用于很多页面时，外部样式表将是理想的选择。在使用外部样式表的情况下，你可以通过改变一个文件来改变整个站点的外观。每个页面使用 <link> 标签链接到样式表。<link> 标签在（文档的）头部：
```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```
浏览器会从文件 `mystyle.css` 中读到样式声明，并根据它来格式文档。

外部样式表可以在任何文本编辑器中进行编辑。文件不能包含任何的 `html `标签。样式表应该以` .css` 扩展名进行保存。下面是一个样式表文件的例子：
```css
hr {color: sienna;}
p {margin-left: 20px;}
body {background-image: url("images/back40.gif");}
```
不要在属性值与单位之间留有空格。假如你使用 “margin-left: 20 px” 而不是 “margin-left: 20px” ，它仅在 IE 6 中有效，但是在 Mozilla/Firefox 或 Netscape 中却无法正常工作。

###内部样式表
当单个文档需要特殊的样式时，就应该使用内部样式表。你可以使用 `<style> `标签在文档头部定义内部样式表，就像这样:
```html
<head>
<style type="text/css">
  hr {color: sienna;}
  p {margin-left: 20px;}
  body {background-image: url("images/back40.gif");}
</style>
</head>
```

###内联样式

由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势。请慎用这种方法，例如当样式仅需要在一个元素上应用一次时。

要使用内联样式，你需要在相关的标签内使用样式（style）属性。Style 属性可以包含任何 CSS 属性。本例展示如何改变段落的颜色和左外边距：
```html
<p style="color: sienna; margin-left: 20px">
This is a paragraph
</p>
```
多重样式
如果某些属性在不同的样式表中被同样的选择器定义，那么属性值将从更具体的样式表中被继承过来。

例如，外部样式表拥有针对 h3 选择器的三个属性：
```css
h3 {
  color: red;
  text-align: left;
  font-size: 8pt;
  }
```
而内部样式表拥有针对 h3 选择器的两个属性：
```css
h3 {
  text-align: right; 
  font-size: 20pt;
  }
```
假如拥有内部样式表的这个页面同时与外部样式表链接，那么 `h3` 得到的样式是：
```css
color: red; 
text-align: right; 
font-size: 20pt;
```
即颜色属性将被继承于外部样式表，而文字排列（text-alignment）和字体尺寸（font-size）会被内部样式表中的规则取代。
<div class="warning"><p>这是警告</p></div>