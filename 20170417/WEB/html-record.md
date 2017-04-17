## what is HTML
- it is not a programmar language, it is a **markup language**
- **markup language** is contented a set of **markup tag**

## HTML tag
- the form of tag is like: <b>keyword </b>
- <b> is the begin of tag, </b> is the end of tag

## meaning of tag
- `<html>...</html>` 之间的文本描述网页
- `<body>...</body>` 之间的文本是可见的页面内容
- `<h1>...</h1>` 显示标题 从h1-h6逐渐变小
- `<p>...</p>` 显示为段落，直接写文本浏览器不会识别换行符
- `<a href="url">...</a>` 网址链接 href为属性, 每个标记中可能会一些属性
- `<br />` 空文件，换行
- `<hr />` 定义水平线
- `k<sub>sub</sub>` 下标

## the attribute of tag
- `<h1 align="center">` 标题居中，align为位置属性
- `<body bgcolor="yellow">` 背景为黄色， bgcolor为背景属性
- `<h1 style="background-color:green">` style 提供了一种改变所有html元素样式的通用方法
**例子:** `<p style="font-family:arial;color:red;font-size:20px;">A paragraph.</p>`

## CSS样式表
使用<style>和<div>配合使用
例子：
在style中定义了header和section两中样式
```
<style>
#header {
background-color:black;
color:white;
text-align:center;
padding:5px;
}
#section {
width:550px;
float:left;
padding:10px;
}
</style>
使用<div id="xxx">...</div>调用定义好的样式
<div id="header">
    geekz93
</div>
<div id="section">
    <h2>Title1</h2>
    不用设置样式了～～
</div>
```
## HTML表单
用于收集不同类型的用户输入
### <form> ... </form>
### 在form下的内容

### type
- text: 输入文本：
` <input type="text" name="beg" value="default"> type:`指定表单的类型，name: 保存数据的变量名, value: 指定默认值

- radio: 选项，定义可选输入
` <input type="radio" name="list1" value="tutu">tutu`

- submit: 向后台程序提交表单， 后台程序由<form>的action属性定义
先在<form>中设置好action的值，即设置表单数据传到哪个脚本上处理
`<form action="/action_page.py">`
定义提交按钮
`<input type="submit" value="Submit">`
