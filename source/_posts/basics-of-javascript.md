---
title: JavaScript从入门到精通：基础应用
date: 2018-1-6 20:22:20
tags: [JavaScript]
---

### JavaScript基础
#### JavaScript组成
- ECMAScript：翻译器/解释器，人类语言与计算机的0,1相互转换
- DOM：Document Object Model，文档对象模型，操作HTML（document）
- BOM：Browser Object Model，浏览器对象模型，操作浏览器（window）

兼容性：
- ECMA：几乎没有兼容性问题
- DOM：有一些操作不兼容
- BOM： 没有兼容问题（完全不兼容）

#### 变量类型
```js
var a=12;
alert(typeof a); //number
// var a='你好';
// alert(typeof a); //string
// var a=true;
// alert(typeof a); //boolean
// var a=function(){};
// alert(typeof a); //function
// var a=document;
// alert(typeof a); //object
// alert(typeof c); //undefined
// var a;
// alert(typeof a); //undefined
```
用`typeof`可以看变量值的类型。

- number 数字
- string 字符串
- boolean 布尔值
- function 函数
- object 对象
- undefined 未定义，或定义了但未给值

变量本身没有类型，变量值才有类型，一个变量应该只存放一种类型的数据。

##### 类型转换：
###### 显示类型转换（强制类型转换）
1、`parseInt()`：从左到右扫描，遇到非数字跳出，输出前面的**整数**。
```js
var a='12px34';
alert(parseInt(a));//结果是12
```

2、`parseFloat()`：如果要输出小数，则用parseFloat。
```js
var a='0.2';
alert(parseFloat(a)); //结果是0.2
//alert(parseInt(a)); //结果是0
```

3、`NaN`：Not a Number，非数字。
```js
var a='abc';
alert(parseInt(a)); //结果是NaN
```
`isNaN`：判断一个值是否为非数字。
```js
var a='bfc';
alert(isNaN(a)); //true
```

###### 隐式类型转换
1、`==`：双等号，会转换类型，再进行比较。
`===`：三等号，比较懒，不换转类型，直接进行比较。
```js
var a=1; //数字
var b='1'; //字符串
alert (a==b); //true，先转换类型，再进行比较
alert (a===b); //false，不转换类型，直接比较
```

2、`-`：减法在函数中的作用就是数字相减，所以使用时会先将两边的值转换成数字。
```js
var a='12';
var b='5';
alert (a+b); //125，加法：1、连接字符串 2、数字相加
alert (a-b); //7，减法：只应用于数字相减，这里先转换了类型
```

##### 案例：求和
```html
<script type="text/javascript">
    window.onload = function() {
        var oTxt1 = document.getElementById('txt1');
        var oTxt2 = document.getElementById('txt2');
        var oBtn1 = document.getElementById('btn1');
        
        oBtn1.onclick = function() {
          var n1=parseFloat(oTxt1.value); //类型转换
          var n2=parseFloat(oTxt2.value);

            if (isNaN(n1)) { //判断第一个框中是否为非数字
                alert('第一个输入框填写的不是数字');
            } else if (isNaN(n2)) { //判断第二个框中是否为非数字
                alert('第二个输入框填写的不是数字');
            } else {
                alert(n1+n2);
            }
        }
    }
</script>
<input id="txt1" type="text">
<input id="txt2" type="text">
<input id="btn1" type="button" value="求和">
```

#### 变量作用域和闭包
##### 变量作用域（作用范围）
- 局部变量，只能在定义它的函数里面使用
- 全局变量，在任何地方都能用，定义在所有函数外

如上面求和的案例，n1、n2是局部变量，只能在定义它们的oBtn1.onclick函数中使用，如果在其他函数中直接用n1、n2，浏览器会报错这两个变量未定义。

##### 闭包
- 子函数可以使用父函数中的局部变量

如上面求和的案例，实际上oTxt1、oTxt2、oBtn1是window.onload的局部变量，而oBtn1.onclick是window.onload的子函数，所以它可以使用oTxt1、oTxt2、oBtn1。

#### 命名规范（匈牙利命名法）
匈牙利命名法：类型前缀+首字母大写

类型|前缀|类型|实例
---|---|---|---
数组|a|Array|aItems
布尔值|b|Boolean|bIsComplete
浮点数|f|Float|fPrice
函数|fn|Function|fnHandler
整数|i|Integer|iItemCount
对象|o|Object|oDiv1
正则表达式|re|RegExp|reEmailCheck
字符串|s|String|sUserName
变体变量|v|variant|vAnything

#### 运算符
1、**算术**：`+`加、`-`减、`*`乘、`/`除、`%`取模（求余数）
```js
alert(7%2); //结果是1
```

2、**赋值**：`=`、`+=`、`-=`、`*=`、`/=`、`%=`
```js
i=i+1
i+=1
i++
//三者的作用是一样的，每次加1
i=i+3
i+=3
//每次加3，后面-=等用法类似
```

3、**关系**：`<`、`>`、`<=`、`>=`、`==`、`===`、`!=`、`!==`。

4、**逻辑**：`&&`与/并且、`||`或、`!`否

5、**运算符优先级**：括号

#### 程序流程控制
1、**判断**：if、switch、?:（三目/三元运算符，是if else的简写）
```js
if (条件1) {
    语句1
}
else if (条件2) {
    语句2
} //可以有无数个else if
else {
    语句n //以上条件都不成立时执行else里的语句
}
```

```js
条件1?语句1:语句2
```

```js
var a=-1;
// if (a%2==0) {
//   alert('双数');
// }
// else {
//   alert('单数');
// }
a%2==0?alert('双数'):alert('单数');
//条件语句很长时，不建议使用三目，看起来会很乱
```

```js
switch (变量){
    case 值1; //变量符合值1，执行语句1，然后跳出
        语句1;
        break;
    case 值2; //值1不符合时，验证值2
        语句2;
        break;
    ......
    default: //以上都不符合，使用默认语句
        语句n;
}
```

```js
var name = 'abc';
var sex = '女';

switch (sex) {
    case '女':
        alert(name + '女士，你好');
        break;
    case '男':
        alert(name + '先生，你好');
        break;
    default:
        alert(name + '你好');
}
```

2、**循环**：while、for

3、**跳出**：break、continue
break：整个循环中断了
continue：本次循环中断，继续下面的循环

4、**什么是真、什么是假**：
真：true、非零数字、非空字符串、非空对象
假：false、数字零、空字符串、空对象、undefined

#### JSON
##### JSON是什么？
JSON，JavaScript Object Notation，JS数据交换语言，和数组差不多，是用来存数据的。

##### JSON和数组
类型|格式|下标|长度|循环
---|---|---|---|---
JSON|`var json={a:12, b:7, c:5}`|字符串|没有length|for in
数组|`var arr=[12, 7, 5]`|数字|有length|建议使用 for 0 - len

##### for in
```js
var arr=[12, 7, 5];

for (var i in arr)
{
    alert('第'+i+'个东西：'+arr[i]);
}
```

```js
var json={a:12, b:7, c:5};

for (var i in json)
{
    alert('第'+i+'个东西：'+json[i]);
}
```


### 深入JavaScript基础

#### 函数返回值
- 函数返回值是函数的执行结果
- 可以没有return
- 一个函数应该只返回一种类型的值

#### 函数传参
arguments：不定参、可变参
```js
function sum() {
  var result=0;
  for (var i=0; i<arguments.length; i++) {
    result+=arguments[i];
  }
  return result;
}
alert(sum(1,3,5,7)); //arguments就代表这里的多个参数，可以是1个，2个，n个
```

示例：取行间样式：
```html
<script>
function getStyle(obj, name, value){
  if (arguments.length==2) {
    return (obj.style[name]);
  }
  else {
    obj.style[name]=value;
  }
}
window.onload=function (){
  var oDiv=document.getElementById('div1');
  alert(getStyle(oDiv, 'width'));
}
</script>
<div id="div1" style="width: 200px; height: 200px; 
background: #000;"></div>
```

拓展：取非行间样式(不能用来设置):
`obj.currentStyle[attr]`在IE中可用；
`getComputedStyle(obj,false)[attr]`在Chrome、Firefox中可用。

```js
function getStyle(obj, name) {
  if (obj.currentStyle) {
    //IE
    return obj.currentStyle[name];
  }
  else {
    //chrome, firefox
    return getComputedStyle(obj, false)[name];
  }
}
window.onload=function(){
  var oDiv=document.getElementById('div1');
  alert(getStyle(oDiv, 'backgroundColor'));
}
```

注意：以上去行间样式的方式只能取但一样式。
复合样式：background（包括backgroundColor、backgroundImage、backgroundRepeat等）、border等。
单一样式：width、height等。

#### 数组基础
- **定义**：数组，是无序的元素序列。
- **格式**：没有任何差别，`[]`的性能略高，因为代码短
  - `var arr=[12, 5, 8, 9];`
  - `var arr=new Array(12, 5, 8, 9)`
- **属性**：length即可以获取，又可以设置，eg.`arr.length=2`将数组长度设为2，`arr.length=0`清空数组。
- **使用原则**：数组中应该只存一种类型的变量。

##### 添加、删除
1、从尾部添加、删除
- push(元素)，从尾部添加
- pop()，从尾部弹出


```js
var arr=[1,2,3];
arr.push(4);
alert(arr); //[1,2,3,4]
```

```js
var arr=[1,2,3];
arr.pop();
alert(arr); //[1,2]
```

2、从头部添加、删除
- unshift(元素)，从头部添加
- shift()，从头部弹出

```js
var arr=[1,2,3];
arr.unshift(11);
alert(arr); //[11,1,2,3]
```

```js
var arr=[1,2,3];
arr.shift();
alert(arr); //[2,3]
```

3、从中间添加、删除
- 删除：splice(起点,长度)
- 插入：splice(起点,0,元素...)
- 综合/替换：splice(起点,长度,元素..)

```js
var arr=[1,2,3,4];
arr.splice(1,2); //以第2个元素为起点，删除2个元素（包含起点元素）
alert(arr); //[1,4]
```

```js
var arr=[1,2,3,4];
arr.splice(3,0,'a','b');//以第4个元素为起点，在其前面插入元素'a','b'
alert(arr); //[1,2,3,'a','b',4]
```

```js
var arr=[1,2,3,4];
arr.splice(1,2,'a','b'); //以第2个元素为起点，删除2个元素，插入两个元素
alert(arr); //[1,'a','b',4]
```

##### 排序、转换
1、排序
排序一个字符串数组：`数组.sort()`
```js
var a=['width', 'height', 'float', 'a'];
alert(a.sort()); //['a', 'float', 'height', 'width']
```

排序一个数字数组：`数组.sort([比较函数])`
```js
var a=[11, 2, 8, 112];
alert(a.sort(function(n1,n2){
    return n1-n2;
    })); //[2,8,11,112]
```

2、连接两个数组
`数组1.concat(数组2)`，注意这里的英文单词是concat，不是contact，意思是合并多个数组、合并多个字符串。
```js
var a=[1,2,3];
var b=[4,5,6];
alert(b.concat(a)); //[4,5,6,1,2,3]
```

3、添加分隔符
`数组.join(分隔符)`，组合数组元素，生成字符串
```js
var a=[1,2,3,4];
alert(a.join('--'));//[1--2--3--4]
```

### 定时器的使用
#### 开启定时器
1、setInterval 间隔型：每隔一段时间执行某个函数（多次）
```js
function show(){
    alert('a');
}
setInterval(show, 1000); //每隔1秒执行show函数一次
```

2、setTimeout  延时型：过一段时间后执行一次某函数（一次）
```js
function show() {
    alert('a');
}
setTimeout(show, 1000); //1秒后执行show函数
```

#### 停止定时器
1、clearInterval：关闭某个间隔型定时器
```html
<script>
    window.onload=function(){
      var oBtn1=document.getElementById('btn1');
      var oBtn2=document.getElementById('btn2');
      var timer=null;

      oBtn1.onclick=function (){
        timer=setInterval(function(){
          alert('a');
        }, 1000);
      }
      oBtn2.onclick=function (){
        clearInterval(timer);
      }
    }
</script>
<input id="btn1" type="button" value="开启">
<input id="btn2" type="button" value="关闭">
```

2、clearTimeout：关闭某个延时型定时器，见延时提示框例子

#### 案例：数码时钟
1、布局：图片0-9展示时间
2、获取系统时间
```js
var oDate=new Date();
alert(oDate.getHours());//当前系统时间小时数,eg.18
alert(oDate.getMinutes());//当前系统时间分钟数,eg.6
alert(oDate.getSeconds());//当前系统时间秒数,eg.12
alert(oDate.getFullYear());//当前系统时间年份，eg.2018
alert(oDate.getMonth()+1);//当前系统时间月份，由于是从0开始的，所以+1
alert(oDate.getDate());//当前日期，eg.6
alert(oDate.getDay());//当前星期X，0是周日，1是周一，以此类推
```

3、显示系统时间
- 字符串连接，见例子中的str变量，连接时间字符串
- 空位补零，见例子中的toDou函数，将时间数字转换成两位数的字符串

4、根据字符串修改图片路径，每隔一秒执行一次
- 修改图片路径，见例子的tick函数，循环匹配字符串与图片路径，`charAt()`具有更好的兼容性，所以使用`str.charAt(i)`，而不是`str[i]`。
- 间隔定时器，setInterval()每秒执行一次tick
- 在定时器的前面先执行一次tick，避免刷新时回归到页面初始的00:00:00。

```html
<head>
  <script>
    function toDou(n) {
      if (n<10) {
        return '0'+n; //小于10的值在前面加一个零
      }
      else {
        return ''+n; //加空字符串使返回的值类型为字符串
      }
    }

    window.onload=function() {
      var aImg=document.getElementsByTagName('img');

      function tick(){ //tick:获取当前时间并修改对应图片地址
        var oDate=new Date();
        var str=toDou(oDate.getHours())+toDou(oDate.getMinutes())+
        toDou(oDate.getSeconds());

        for (var i=0; i<str.length; i++) {
        aImg[i].src='images/'+str.charAt(i)+'.png';
        };
      }

      setInterval(tick, 1000); //每隔一秒执行一次tick
      tick(); //先执行一次tick，避免刷新时回到00:00:00
    }
  </script>
</head>
<body style="font-size: 50px; color: #fff; background: #000;">
  <img src="images/0.png">
  <img src="images/0.png">
  :
  <img src="images/0.png">
  <img src="images/0.png">
  :
  <img src="images/0.png">
  <img src="images/0.png">
</body>
```

#### 案例：延时提示框
- 布局：头像框和信息框，信息框默认隐藏
- 效果：鼠标放到头像上，显示信息框；鼠标移出头像，信息框延迟隐藏；鼠标放到信息框上，解除信息框的延迟隐藏；鼠标移出信息框，恢复其延迟隐藏。也就是：鼠标在头像上和在信息框上，信息框都是一直显示的；鼠标移出头像或信息框时，信息框延时隐藏。

```html
<script>
window.onload = function() {
    var oDiv1 = document.getElementById('div1');
    var oDiv2 = document.getElementById('div2');
    var timer = null;

    oDiv1.onmouseover = oDiv2.onmouseover = function() {
        clearTimeout(timer);
        oDiv2.style.display = 'block';
    }
    oDiv1.onmouseout = oDiv2.onmouseout = function() {
        timer = setTimeout(function() {
            oDiv2.style.display = 'none';
        }, 1000);
    }
}
</script>
<div id="div1"></div>
<div id="div2"></div>
</body>
```

#### 案例：无缝滚动
- 布局：div>ul>li*4，整个ul移动
- 运动原理：通过定时器改变ul的left。（可以通过offsetLeft获取对象的左侧距离，通过offsetWidth获取对象的宽度；offsetTop与offsetHeight以此类推。）
- 复制li：当ul原有的li向一侧运动完后，复制的li无缝连接起来。
- 运动到一半时拉回原点：这样视觉范围内，ul一直首尾相连。
- 鼠标移入移出：关闭或打开定时器。
- 向左向右移动按钮：改变运动值的正负（向右/向左）和大小（移动快慢）。

```html
<script>
window.onload = function() {
    var oDiv = document.getElementById('div1');
    var oUl = document.getElementsByTagName('ul')[0];
    var aLi = document.getElementsByTagName('li');
    var speed = -2; //默认向左移动
    oUl.innerHTML += oUl.innerHTML; //复制li
    oUl.style.width = aLi[0].offsetWidth * aLi.length + 'px';//修改ul宽度
    //运动函数：当向左移动一半时，将ul拉回原点；
    //向右移动一半时（left即将>0），将ul拉回原点
    function move() {
        if (oUl.offsetLeft < -oUl.offsetWidth / 2) {
            oUl.style.left = '0';
        }
        if (oUl.offsetLeft > 0) {
            oUl.style.left = -oUl.offsetWidth / 2 + 'px';
        }
        oUl.style.left = oUl.offsetLeft + speed + 'px';
    }
    var timer = setInterval(move, 30); //每30毫秒执行运动函数一次
    oDiv.onmouseover = function() {
        clearInterval(timer); //鼠标移入div时关闭定时器，停止ul运动
    }
    oDiv.onmouseout = function() {
        timer = setInterval(move, 30); //鼠标移出时恢复运动
    }
    document.getElementsByTagName('a')[0].onclick = function() {
        speed = -2; //向左移动
    }
    document.getElementsByTagName('a')[1].onclick = function() {
        speed = 2; //向右移动
    }
}
</script>
<a href="javascript:;">向左走</a>
<a href="javascript:;">向右走</a>
<div id="div1">
    <ul>
        <li class="li1"></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</div>
```

