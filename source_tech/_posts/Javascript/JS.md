---
title: Javascript
tags:
  - HTML
  - Computer Network
  - JavaScript
categories:
  - study
  - network
  - JavaScript
toc: true
abbrlink: 9809
comment: 'waline'
date: 2024-07-20 00:00:00
---
[来学习吧：www.runoob.com](https://www.runoob.com/js/js-tutorial.html)

<!-- more -->

## JavaScript使用方法与功能

### JS怎么引入

**▶在html中如何写入js**

- 可以将js代码写入`<sciprt>`与`</script>`之间，这个标签可以置于`<head>`或`<body>`标签内
- 也可以在将代码写在js文件中，在`<script>`中使用src属性设置链接，如
  ```html
  <script src="myScript.js"></script>
  ```

<br>

**▶在浏览器中如何调试js**

- 在浏览器中（以Chrome为例），右键选择检查或者按F12打开开发者工具，选择Console/控制台标签，即可输入js代码。点击禁止按钮可以清空内容。
- 此外，点击Sources/源代码/来源标签，在下一级的面板中按`>>`，找到Snippets/代码段 ![](https://www.runoob.com/wp-content/uploads/2020/11/9F5F8D84-9C0D-4F6B-98AF-8B9349118297.jpg)
  就可以编写js文件了。保存后右键文件可以执行代码
  代码示例：
  ```js
  console.log("test")
  console.log("使用 console.log() 可以将内容写入到浏览器的控制台")
  ```

### JS怎么输出

JavaScript 没有任何打印或者输出的函数。
去你的那我怎么知道输出了什么???

### JS怎么显示数据(有区别吗)

- 使用 window.alert() 弹出警告框。
- 使用 document.write() 方法将内容写到 HTML 文档中。
- 使用 innerHTML 写入到 HTML 元素。
- 使用 console.log() 写入到浏览器的控制台。

> **▶console.log()的用处:**
console不会打断你页面的操作，如果用alert弹出来内容，那么页面就死了，但是console输出内容后你页面还可以正常操作。
也可以像 C 语言用 %s字符串、%d整型、%f浮点型 来使用变量，可见[这里](https://blog.csdn.net/u013706540/article/details/82184145)
```js
var hello = 'hello';
var one = 1;

console.log('%s world', hello)
console.log('%d + 1 = 3', one)
```
此外，console.log可以添加显示样式，如
```js
console.log('%cfuck', 'font-size:200px')
```
你甚至可以封装一个函数，定义console传过来文本的样式：
```js
(function() {
    var _log = console.log;
    console.log = function() {
        if (typeof(arguments[0]) != 'object' && typeof(arguments[0]) != 'function' && arguments.length == 1) {
            _log.call(console, '%c' + arguments[0], "text-shadow: 0 1px 0 #ccc,0 2px 0 #c9c9c9,0 3px 0 #bbb,0 4px 0 #b9b9b9,0 5px 0 #aaa,0 6px 1px rgba(0,0,0,.1),0 0 5px rgba(0,0,0,.1),0 1px 3px rgba(0,0,0,.3),0 3px 5px rgba(0,0,0,.2),0 5px 10px rgba(0,0,0,.25),0 10px 10px rgba(0,0,0,.2),0 20px 20px rgba(0,0,0,.15);font-size:5em")
        } else {
            _log.call(console, ...arguments)
        }
    }
})()
```

### JS有啥用

介绍作用同时也顺便介绍一下document.write、alert、document.getElementById几个常用的方法~

```html
<p>
1.JavaScript 能够直接写入 HTML 输出流中：
</p>
<script>
document.write("<h1>这是一个标题</h1>");
document.write("<p>这是一个段落。</p>");
</script>
```
您只能在 HTML 输出流中使用 <strong>document.write</strong>。
> 假如在文章加载后才用函数调用document.write会覆盖html所有其他内容
> ```html
<script>
function myfunction(){
    document.write("使用函数来执行document.write，即在文档加载后再执行这个操作，会实现文档覆盖");
}
document.write("<h1>这是一个标题</h1>");
document.write("<p>这是一个段落。</p>");
</script>
<p>
您只能在 HTML 输出流中使用 <strong>document.write</strong>。
如果您在文档已加载后使用它（比如在函数中），会覆盖整个文档。
</p>
<button type="button" onclick="myfunction()">点击这里</button>
```
<script>
function myfunction(){
    document.write("看到没，使用函数来执行document.write，也就是在文档加载后才执行这个操作，别的全给你整没了");
    document.write("<br>");
    document.write("刷新就可以回去啦");
}
</script>
<a class="btn" onclick="myfunction()">就像这样</a>

---

```html
<p>
2.JavaScript 能够对事件反应(如本例中对按钮onclick事件的反应：alert)
</p>
<button type="button" onclick="alert('欢迎!')">点我!</button>
```
<a class="btn" onclick="alert('JS：你刚刚执行了onclick是不是！老实交代！')">点我!</a>

---

```js
// 3.Javascript 可以更改HTML元素、
x=document.getElementById("demo");  //查找元素
x.innerHTML="Hello JavaScript";    //改变内容
```
`document.getElementById("some id")`是**HTML DOM**中定义的，DOM (Document Object Model)（文档对象模型）是用于访问 HTML 元素的正式 W3C 标准。
```html
<!-- 3.Javascript 可以动态更改HTML元素 -->
<script>
function changeImage()
// 定义函数
{
    element=document.getElementById('myimage')
    // 找到图片元素
    if (element.src.match("bulbon"))
    // 判断灯泡是否为亮的（即src属性中是否有bulbon这个字符串）
    {
        element.src="/images/pic_bulboff.gif";
        // 是则换成灭的
    }
    else
    {
        element.src="/images/pic_bulbon.gif";
        // 不是则换成亮的
    }
}
</script>
<img id="myimage" onclick="changeImage()" src="/images/pic_bulboff.gif" width="100" height="180">
<!-- 图片元素点击时触发函数changeImage() -->
```
```js
// 3.Javascript 可以更改元素属性
=document.getElementById("demo")  //找到元素 
x.style.color="#ff0000";           //改变id为demo的元素的style属性
```

---

```js
// 4.Javascript 可以判断输入
if isNaN(x) {
    alert("不是数字");
}
```

---



## JavaScript语法

### 字面量

在编程语言中，一般固定值称为**字面量**，包括数字、字符串、表达式、数组、对象、函数。
- 数字（Number）字面量 可以是整数或者是小数，或者是科学计数(e)。
- 字符串（String）字面量 可以使用单引号或双引号。
- 表达式字面量 用于计算。
- 数组（Array）字面量 定义一个数组：
  ```js
  [1,14,514]
  ```
- 对象（Object）字面量 定义一个对象：
  ```js
  {firstName:"John",lastName:"Man",age:20000}
  ```
- 函数（Function）字面量 定义一个函数：
  ```js
  function myFunction(a, b) { return a * b;}
  ```

数字，字符串，数组，对象等等称为**数据类型**

### 变量

JavaScript 使用关键字 var 来定义变量， 使用等号来为变量赋值：
```js
var x,length

x = 10086
length = x
```
变量可以通过变量名访问。在指令式语言中，变量通常是可变的。字面量是一个**恒定的值**，变量是一个**可以赋值的名称**

### 操作符

操作符分为赋值、算术和位运算符与条件、比较及逻辑运算符

### 关键字

JavaScript 关键字用于标识要执行的操作。

和其他任何编程语言一样，JavaScript 保留了一些关键字为自己所用。
以下是 JavaScript 中最​​重要的保留关键字：

| 1        | 2          | 3          |
|----------|------------|------------|
| abstract | else       | super        |
| boolean  | enum       | void         |
| break    | export     | volatile     |
| byte     | extends    | while        |
| case     | false      | with         |
| catch    | final      | var          |
| char     | finally    | instanceof   |
| class    | float      | switch       |
| const    | for        | int          |
| continue | function   | synchronized |
| debugger | goto       | protected    |
| default  | if         | public       |
| delete   | implements | return       |
| do       | import     | short        |
| double   | in         | static       |
| interface  | let      | this         |
| long       | throw    | throws       |
| native     | new      | transient    |
| null       | true     | try          |
| package    | private  | typeof       |



JavaScript 对大小写是敏感的。
当编写 JavaScript 语句时，请留意是否关闭大小写切换键。
函数 getElementById 与 getElementbyID 是不同的。
同样，变量 myVariable 与 MyVariable 也是不同的。
