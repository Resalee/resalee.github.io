---
title: JavaScript从入门到精通：初探JavaScript魅力
date: 2018-1-5 16:38:20
tags: [JavaScript]
---
开始学习blue老师的JavaScript从入门到精通系列课程，在此写写笔记。
老师的教学风格是根据实例，循序渐进地讲解，从最原始的行间操作到提取行间操作，从控制单个元素到控制数组，从if到while到for，由浅入深演示（也就演示了其中一些可能会掉的坑）；同时运用很多类比，将js与我们已知的东西联系起来，更好理解。

#### JavaScript是什么？
JavaScript是修改样式的编程语言。

#### JavaScript如何编写？
- 布局：HTML+CSS
- 属性：确定要修改哪些属性
- 事件：确定用户做哪些操作
- 编写JS：在事件中，用JS来修改页面元素的样式

#### 案例介绍
##### 鼠标提示框（事件、属性，函数与变量）
**分析效果实现原理**：
- 样式：提示框的display变化
- 事件：onmouseover，onmouseout，鼠标的进入和移出

```html
<input type="checkbox" onmouseover="document.getElementById('hint').style.display='block';" onmouseout="document.getElementById('hint').style.display='none';"> 
<div id="hint">我写我写写写。。。</div>
```

**知识点**：
1、get.ElementById：通过ID获取元素，需要先获取元素，才能控制元素，不然会出现兼容问题。
2、`=`，等号的含义是“赋值”，也就是将某个值传递给某个参数，可以理解控制参数变成某个值。
3、属性：特性、特点，元素的属性包括宽、高、display等等。
eg.
```
div.颜色=红色
我.性别=女
```

**用函数来改写**：
```javascript
function toShow(){ //定义函数
    var oDiv = document.getElementById('hint'); //获取要控制的元素
    oDiv.style.display = 'block'; //改变元素样式
}
function toHide() {
    var oDiv = document.getElementById('hint');
    oDiv.style.display = 'none';
}
```
```html
<input type="checkbox" onmouseover="toShow()" onmouseout="toHide()"> <!-- 添加鼠标事件，调用函数 -->
<div id="hint">我写我写写写。。。</div>
```

**知识点**：
1、变量：给XX取一个别名。(var=variable，“变量”的英文)
eg.
```
//见到oDiv就等于见到了document.getElementById('hint')
var oDiv = document.getElementById('hint');  
//见到尚方宝剑就等于见到了皇上
var 尚方宝剑 = 皇上;
```
2、函数：
格式：
```
function 函数名() {
    代码
}
函数名()
```
eg.
```JavaScript
function show() //定义，只是告诉系统有这个函数，不会实际执行
{
    alert('abcd');
}
show(); //调用，真正执行函数里的代码
```

##### 网页换肤（JS的操作范围）
**效果实现**：
- 布局：写好HTML和CSS
- 定义函数
- 获取要控制的元素，这里是id为style1的link
- 修改要控制的元素属性，这里是控制link的href，通过替换css文件来修改页面样式，达到换肤的效果
- 调用函数，这里是通过onclick鼠标点击事件调用函数

```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link id="style1" rel="stylesheet" type="text/css" href="css1.css">
    <script type="text/javascript">
    function toRed() {
        var oStyle = document.getElementById('style1');

        oStyle.href = 'css1.css';
    }

    function toGreen() {
        var oStyle = document.getElementById('style1');

        oStyle.href = 'css2.css';
    }
    </script>
</head>

<body>
    <input type="button" value="皮肤1" onclick="toRed()">
    <input type="button" value="皮肤2" onclick="toGreen()">
    <div id="div1"></div>
</body>
```

**知识点**：
- 任何标签都可以加ID，包括link
- 任何标签的任何属性，都可以修改
- HTML里怎么写，JS里就怎么写（class除外，要使用className）

```
//给元素赋予class类名
oDiv.className='box';
```

##### 显示隐藏（if函数）
```html
    <style type="text/css">
    #div1 {
        display: none;
        width: 100px;
        height: 200px;
        border: 1px solid #ddd;
        background: #999;
    }
    </style>
    <script type="text/javascript">
    function showHide() {
        var oDiv = document.getElementById('div1');

        if (oDiv.style.display == 'block') { //易错点：这里是双等号
            oDiv.style.display = 'none';
        } else {
            oDiv.style.display = 'block';
        }
    }
    </script>
    <input type="button" value="显示隐藏" onclick="showHide()">
    <div id="div1"></div>
```

**知识点**：
1、if函数，判断条件是否成立，成立时执行语句1，否则执行语句2。
格式：
```
if (条件) {
    语句1
}
else {
    语句2
}
```
eg.
```
if (预报有雨) {
    带伞
}
else {
    不带伞
}
```

2、`==`，双等号的含义就是“等于”，自己写这一段的时候就写成了`=`，结果无效，因为条件是display等于block，而不是赋值，将display改成block。

##### div变色（函数传参）
```html
<script>
    function changeColor(color) {
      var oDiv = document.getElementById('div1');

      oDiv.style.background=color;
    }
  </script>
  <input type="button" value="变绿" onclick="changeColor('green')">
  <input type="button" value="变黄" onclick="changeColor('yellow')">
  <input type="button" value="变黑" onclick="changeColor('black')">
  <div id="div1"></div>
```
**知识点**：
函数传参：参数是占位符，当函数里有定不下来的东西的时候，可以用参数，比如例子里的颜色，先用color占位，然后在调用函数时给参数具体的值。
可以赋予函数多个参数：

```html
<style>
    #div1 {
      width: 200px;
      height: 200px;
      background: red;
    }
  </style>
  <script>
    function changeStyle(name, value) {
      var oDiv = document.getElementById('div1');

      oDiv.style[name]=value;
    }
  </script>
   <input type="button" value="变宽" onclick="changeStyle('width', '300px')">
  <input type="button" value="变高" onclick="changeStyle('height', '300px')">
  <input type="button" value="变绿" onclick="changeStyle('background', 'green')">
  <div id="div1">
  </div>
```

**知识点**：
1、操作属性的两种方法
- 元素.style.属性=XX；
- 元素.style[属性变量/'属性名']=XX；

所有可以用`.`的地方都可以用`[]`代替，第二种方法比较适合属性名不确定的时候。
eg.
```
oDiv['style'][name]=value;
```

2、变量和字符串的区别
变量：变量的值是可以变的，如果没有对变量赋值，你不知道变量是什么值。
常量/字面量：看到什么就是什么，比如数字12，就是12，字符串'bac'就是bac。
变量不需要加引号，不然会被解读成字符串，而字符串的值是确定的。

3、style与className
- 元素.style.属性=xxx是修改行间样式，权重最高
- 之后再修改className不会有效果

所以style与className不要混着用，容易出现问题。

##### 提取行间事件
```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
    #hint {
        display: none;
        width: 100px;
        height: 200px;
        border: 1px solid #ddd;
        background: #eee;
    }
    </style>
    <script type="text/javascript">
    window.onload=function(){
        var oCh = document.getElementById('btn1');
        var oDiv = document.getElementById('hint');

        oCh.onmouseover = function() {
            oDiv.style.display = 'block';
        }
        oCh.onmouseout = function() {
            oDiv.style.display = 'none';
        }
    }
    </script>
</head>

<body>
    <input id="btn1" type="checkbox">
    <div id="hint">我写我写写写。。。</div>
</body>
```
**知识点**：
1、用JS添加事件，和JS添加属性一样：
```
oCh.title='abc'; //给oCh元素添加title，值为abc
oCh.onclick=XX函数; //给oCh元素添加onclick事件，调用XX函数
```
这样的好处是不用在行间添加事件，将行为（js）、样式（css）、结构（html）三者分离，在操作较多元素时，减轻工作量，而且方便修改，利于团队合作。

2、匿名函数
给函数命名并调用：
```js
function (a) {
    oDiv.style.display='none';
}
oCh.onclick=a; //调用函数a
```
不给函数命名直接调用，这时的函数就叫匿名函数，没有名字：
```js
oCh.onclick=function () {
    oDiv.style.display='none';
}
```

3、window.onload的作用是等页面加载完后，再执行里面的代码。
不然如示例中，js在body内容的上面，浏览器先读取到js，但找不到对应的元素（还未加载）来执行，就会报错。

##### 数组与循环
```html
<script type="text/javascript">
    window.onload=function() {
      var oDiv=document.getElementsByTagName('div');

      for (var i=0; i<oDiv.length; i++) { //我的错误：一开始没写var，二是把分号写成了逗号
        oDiv[i].style.background='green';
      }
    }
  </script>
  <div></div>
  <div></div>
  <div></div>
  <div></div>
```

**知识点**：
1、getElementsByTagName，按标签类型提取元素
注意这里的elements是复数，如果有多个同类元素（如示例的div），这时就提取出多个元素（div）。

2、数组
数组类似压缩包，看着是一个文件，但里面包含了多个文件。上面getElementsByTagName提取出的元素就是一个数组，里面包含多个元素。
数组的表示方式：用方括号`[元素1, 元素2, 元素3, 元素4]`,但数组的计数方式是从0开始的，也就是`元素1`的表示方式是：`数组名[0]`，`元素4`的表示方式是`数组名[3]`。
数组的长度：`数组名.length`,如示例中的`oDiv.length`就是4。

3、循环
先看if函数，条件成立时，执行一次：
```js
if (条件) {
    语句; //条件成立时，if函数执行一次
}
```
再看while函数，条件成立时，执行多次：
```js
var i=0;                     //1.初始化
while (i<5) {          //2.条件
    alert(i);             //3.语句，条件成立时，一直执行
    i++;                        //4.自增，这里也可以表示为i=i+1，执行完一次，i的值就加1
}
```
再看for函数，作用与while一样，条件成立时，执行多次，但格式更简单：
```js
for (var i=0; i<5; i++){  //1.初始化，条件，自增
    alert(i);                           //2.语句
}
```

##### 选项卡
```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    #choose .active {
        background: yellow;
    }

    #choose div {
        display: none;
        width: 200px;
        height: 300px;
        background: green;
        border: 1px solid #ddd;
    }
    </style>
    <script>
    window.onload = function() {
        var oDiv = document.getElementById('choose');
        var aBtn = oDiv.getElementsByTagName('input');
        var aDiv = oDiv.getElementsByTagName('div');

        for (var i = 0; i < aBtn.length; i++) {
            aBtn[i].index = i;
            aBtn[i].onclick = function() {
                for (var i = 0; i < aBtn.length; i++) {
                    aBtn[i].className = '';
                    aDiv[i].style.display = 'none';
                }
                this.className = 'active';
                aDiv[this.index].style.display = 'block';
            }
        }
    }
    </script>
</head>

<body>
    <div id="choose">
        <input class="active" type="button" value="教育">
        <input type="button" value="培训">
        <input type="button" value="招生">
        <input type="button" value="出国">
        <div style="display: block;">111111</div>
        <div>222222</div>
        <div>333333</div>
        <div>444444</div>
    </div>
</body>
```

**知识点**：
1、实现思路：
- 写HTML+CSS，第一个按钮和对应的div展示出点击后的效果
- 获取元素，包括所有的按钮，和所有对应的div
- 事件效果，点击时按钮变黄，出现对应的div，其他按钮恢复默认背景，div隐藏
- js实现，点击时先取消所有按钮的效果和div效果，然后赋予当前点击的按钮背景和div展示

2、this：当前发生事件的元素

3、index：如果将index直接放到HTML中，将出现兼容问题，因为这是一个自定义的属性。
但是可以通过js来设置这个自定义属性，并且可以通过循环设置实现。

##### JS简易日历（innerHTML）
```html
 <script>
    window.onload = function() {
        var arr = ['1月去干啥', '2月去春游', '3月去爬山', '4月去野炊', '5月去大明湖', '6月去哈尔滨', '7月去昆明大理', '8月家里蹲', '9月开学啦', '10月好好学习天天向上', '11月加油考试', '12月写总结，哈哈哈'] //我的坑：没加单引号

        var tab = document.getElementById('tab');
        var aBtn = tab.getElementsByTagName('li');
        var text = tab.getElementsByTagName('div')[0]; 
        //我的坑：没加下标，下面作为数组（而不是数组中的一个元素）调用是无法改变样式的

        for (var i = 0; i < aBtn.length; i++) {
            aBtn[i].index = i;
            aBtn[i].onmouseover = function() {
                for (var i = 0; i < aBtn.length; i++) {
                    aBtn[i].className = '';
                }
                this.className = 'active';
                text.innerHTML = '<h2>' + (this.index + 1) + '月活动</h2><p>' + arr[this.index] + '</p>';
            }
        }
    }
    </script>
    <div id="tab" class="calendar">
    <ul>
        <li class="active"><h2>1</h2><p>JAN</p></li>
        <li><h2>2</h2><p>FER</p></li>
        <li><h2>3</h2><p>MAR</p></li>
        <li><h2>4</h2><p>APR</p></li>
        <li><h2>5</h2><p>MAY</p></li>
        <li><h2>6</h2><p>JUN</p></li>
        <li><h2>7</h2><p>JUL</p></li>
        <li><h2>8</h2><p>AUG</p></li>
        <li><h2>9</h2><p>SEP</p></li>
        <li><h2>10</h2><p>OCT</p></li>
        <li><h2>11</h2><p>NOV</p></li>
        <li><h2>12</h2><p>DEC</p></li>
    </ul>
    <div class="text">
        <h2>1月活动</h2>
        <p>快过年了，大家可以商量着去哪玩吧～</p>
    </div>
</div>
```
**知识点**：
1、innerHTML：设置标签里的内容，可以放HTML结构内容，如示例里的div里不仅放了文字，还放了h2和p标签。

2、数组的应用：这里和上面选项卡的区别是只有一个div，然后通过数组调取内容。

3、字符串连接：默认连接是第一个+第二个，然后前面两个相加的结果+第三个，可以用括号来提高优先级。
```
'abc'+12+5='abc12'+5='abc125'
'abc'+(12+5)='abc'+17='abc17'
```

***
课程资源：[智能社：JavaScript教程-从入门到精通](http://study.163.com/course/introduction.htm?courseId=224014#/courseDetail?tab=1)

