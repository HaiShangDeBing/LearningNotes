# JavaScript

[TOC]



## JavaScript语法规范

### 1 JavaScript 书写位置

1. 与css类似，直接嵌入到html页面中.

   ![1](E:\Picture\javascript\1.png)

2. 文件调用：JavaScript代码写到另一个文件当中（其后缀通常为“.js”），然后用格式为“<script

src="javascript.js"></script>”的标记把它嵌入到文档中.

![2](E:\Picture\javascript\2.png)

html页面中出现<script>标签后，就会让页面暂停等待脚本的解析和执行。无论当前脚本是内嵌式还是外链式，页面的下载和渲染都必须停下来等待脚本的执行完成才能继续，这在页面的生命周期中是必须的。

### 2 JavaScript 网页中输出信息写法

1. alert()，在网页中弹出提示框，显示信息。
2. console.log()，在控制台输出消息，一般用来调试程序。
3. prompt()，在网页中弹出输入框，一般用来接收用户输入信息。
4. confirm()，在网页中弹出提示框，显示信息，该方法一般与if 判断语句结合使用。
5. document.write()，直接在页面中输出信息。

### 3 声明变量（定义变量）  var

变量定义：   var   自定义名称;

**命名规范：**

- 变量名必须以字符或下划线“_”开头
- 变量可以包含数字、从A至Z的大小字母
- JavaScript严格区分大小写，computer和Computer是两个完全不同的变量
- 禁止使用JavaScript的保留关键字作为变量名

![3](E:\Picture\javascript\3.png)

![4](E:\Picture\javascript\4.png)

### 4 JavaScript中数据类型

#### 简单数据类型：

- Number:数字类型
- String:字符串类型
- Boolean:布尔类型
- undefined:变量未初始化
- null：空类型

#### 复杂数据类型：

- Object:对象（引用）
- Array:数组

**NaN**:  Not  a Number      表示不是一个数字，判断是不是一个数字使用：   isNaN(x)

**Infinity**：无穷大          例如： var   number=7/0 ;

#### 类型转换

```javascript
var a="3.14";
var b=a-2;//输出b等于1.14
var c=a+2;//输出c等于3.142
```

- 对于减号运算符，因为字符串不支持减法运算，所以系统自动将字符串转换成数值，对于包含其他字符的字符的字符串，将转换成NaN。
- 对于加号运算符，因为字符串可用加号作为连接运算符，所以系统自动将数值转换成字符串。

![5](E:\Picture\javascript\5.png)

JavaScript 提供了如下几个函数来执行强制类型转换：

- toString():将布尔值、数值等转换成字符串
- parseInt():将字符串、布尔值等转换成整数
- parseFloat():将字符串、布尔值等转换成浮点数

#### 字符串类型

JavaScript 的字符串必须用引号括起来，可以是单引号，也可以是双引号。有如下基本方法和属性操作字符串。

- String()：可以构建一个字符串
- charAt()：获取字符串特定索引处的字符
- charCodeAt()：返回字符串中特定索引处的字符所对应的Unicode的值
- length：返回字符串长度
- toUpperCase()：转换成大写字母
- toLowerCase()：转换成小写字母
- fromCharCode()：将一系列Unicode值转换成字符串
- indexOf()：返回字符串中特定字符串第一次出现的位置
- lastIndexOf()：返回字符串中特定字符串最后一次出现的位置
- substring()：返回字符串的某个子串
- slice()：返回字符串的某个子串，功能比substring更强大支持负数参数
- match()：使用正则表达式搜索目标子字符串
- search()：使用正则表达式搜索目标子字符串
- concat()：用于将多个字符串拼加成一个字符串
- split()：将某个字符串分隔成多个字符串，可以指定分隔符
- replace()：将字符串中某个子串以特定字符串替代

#### typeof和instanceof运算符

typeof用于判断某个变量的数据类型，instanceof用于判断某个变量是否为指定类的实例

![17](E:\Picture\javascript\17.png)

![18](E:\Picture\javascript\18.png)

### 5 语句

#### 语句块

```javascript
{
  x=Math.PI;
}
```

JavaScript要求所有的语句都以分号结束，但语句块不需要以分号结束，且语句块中每个语句都需要以分号结束。

#### 异常抛出语句

`throw new Error(errorString);`

```html
<!DOCTYPE html>
<html>
<body>

<script>
function myFunction()
{
try
{ 
var x=document.getElementById("demo").value;
if(x=="")    throw "值为空";
if(isNaN(x)) throw "不是数字";
if(x>10)     throw "太大";
if(x<5)      throw "太小";
}
catch(err)
{
var y=document.getElementById("mess");
y.innerHTML="错误：" + err + "。";
}
}
</script>

<h1>我的第一个 JavaScript 程序</h1>
<p>请输入 5 到 10 之间的数字：</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">测试输入值</button>
<p id="mess"></p>

</body>
</html>
```

#### 异常捕捉语句

```javascript
try
{
  statements
}
catch(e)
{
  statements
}
finally
{
  statements
}
```

```html
<!DOCTYPE html>
<html>
<head>
<script>
var txt="";
function message()
{
try
  {
  adddlert("Welcome guest!");
  }
catch(err)
  {
  txt="本页有一个错误。\n\n";
  txt+="错误描述：" + err.message + "\n\n";
  txt+="点击确定继续。\n\n";
  alert(txt);
  }
}
</script>
</head>

<body>
<input type="button" value="查看消息" onclick="message()" />
</body>

</html>

```

#### with 语句

```javascript
with(object)
{
  statements
}
with(document)
{
  writeln("a");
  writeln("b");
  writeln("c");
}
```

可以避免重复书写对象。

![19](E:\Picture\javascript\19.png)

#### for in 循环

```javascript
for (index in object)
{
  
}

var person={fname:"John",lname:"Doe",age:25};
for (x in person)
  {
  txt=txt + person[x];
  }
```

它主要有两个作用：

- 遍历数组里的所有数组元素
- 遍历JavaScript对象的所有属性

### 6 函数

#### 定义命名函数

```javascript
function functionName(parameter list)
{
  statements
}
```

定义匿名函数

```javascript
function (parameter list)
{
  statements
};
```

实际上就是定义了一个函数对象，接下来可以将这个对象赋给另一个变量，然后就可以通过这个变量来调用这个匿名函数。

#### 使用Function类匿名函数

```javascript
var f=new Function('name',"document.writeln('Function定义的函数<br>');"+"document.writeln('你好'+name);");
f("yeefu");
```

当定义一个函数后，实际上得到如下4项

- 函数：就像Java的方法一样，这个函数可以被调用
- 对象：定义一个函数时，系统也会创建一个对象，该对象时Function类的实例
- 方法：定义一个函数时，该函数通常都会附加给某个对象，作为该对象的方法
- 类：在定义函数时，也得到一个与函数同名的类。

因此，当我们定义一个函数时，有如下方式来调用函数：

- 直接调用函数：返回调用函数总是返回该函数体内最后一条return语句的返回值；如果该函数体内不包含return语句，则直接调用函数没有任何返回值。
- 使用new关键字调用函数，通过这种方式调用总有一个返回值，返回值就是一个JavaScript对象。

```javascript
var test=function(name)
{
    return "你好，"+name;
}
var rval=test('lee');//输出rval为你好，lee
var obj=new test('lee');//输出obj为[object Object]

function Person(name,age)
{
    this.name=name;
  	this.age=age;
  	this.info=function()
    {
        document.writeln(this.name);
      	document.writeln(this.age);
    };
}
var p=new Person('lee',24);
p.info();

var hello=function(name)
{
    document.write(name);
}
window.hello("lee");
var p={
    walk:function()
  	{
      for(var i=0;i<2;i++)
        documnet.write("slow");
  	}
}
p.walk();
```

- 以call()方法调用函数

```javascript
/*有些时候调用函数时需要动态传入一个函数引用，此时为了动态地调用函数，就需要使用call方法来调用函数了。
假如定义一个形如each（array,fn)的函数，这个函数可以自动迭代处理array数组元素，而fn函数则负责对数组元素进行处理，此时需要在each函数中调用fn函数，但目前fn函数并未确定，因此无法采用直接调用方法来调用fn函数，此时可以通过call()方法来调用函数。*/
var each=function(array,fn)
{
    for(var index in array)
      {
          fn.call(null,index,array[index]);
      }
}
//调用each函数，第一个参数是数组，第二个参数是函数
each([4,20,3],function(index,ele)
    {
    document.write(index+ele);
})
```

- 以apply()方法调用函数

通过call调用函数时，必须在括号中详细地列出每个参数，通过apply()动态调用函数时，可以在括号里以arguments来代表所有参数。

```javascript
var myfun=function(a,b)
{
  alert(a+b);
}
myfun.call(window,12,23);
var example=function(num1,num2)
{
  myfun.apply(this,arguments);
}
example(20,40);
myfun.apply(window,[12,23]);
```

![20](E:\Picture\javascript\20.png)

![21](E:\Picture\javascript\21.png)

### 7 创建对象

#### 使用new关键字调用构造器创建对象，`var p=new Person();`

#### 使用Object直接创建对象，`var myobj=new Object();`

#### 使用JSON语法创建对象

```javascript
object={
  Name:Value,
  Name:Value,
  ...
}
```


```html
<!--使用对象构造器,本例使用函数来构造对象;-->
<!DOCTYPE html>
<html>
<body>

<script>
function person(firstname,lastname,age,eyecolor)
{
this.firstname=firstname;
this.lastname=lastname;
this.age=age;
this.eyecolor=eyecolor;
}

myFather=new person("Bill","Gates",56,"blue");

document.write(myFather.firstname + " is " + myFather.age + " years old.");
</script>

</body>
</html>
```

![22](E:\Picture\javascript\22.png)

![23](E:\Picture\javascript\23.png)

![25](E:\Picture\javascript\25.png)

现在就更像创建一般对象了。所有的非函数属性都在构造函数中创建，意味着又能够用构造函数的参数赋予属性默认值了。因为只创建 showColor() 函数的一个实例，所以没有内存浪费。此外，给 oCar1 的 drivers 数组添加 "Bill" 值，不会影响到 oCar2 的数组，所以输出这些数组的值时，oCar1.drivers 显示的是 "Mike,John,Bill"，而 oCar2.drivers 显示的是 "Mike,John"。因为使用了原型方式，所以仍然能利用 instanceof 运算符来判断对象的类型。

这种方式是 ECMAScript 采用的主要方式，它具有其他方式的特性，却没有他们的副作用。不过，有些开发者仍觉得这种方法不够完美。

#### **动态原型方法**

![26](E:\Picture\javascript\26.png)

直到检查 typeof Car._initialized 是否等于 "undefined" 之前，这个构造函数都未发生变化。这行代码是动态原型方法中最重要的部分。如果这个值未定义，构造函数将用原型方式继续定义对象的方法，然后把 Car._initialized 设置为 true。如果这个值定义了（它的值为 true 时，typeof 的值为 Boolean），那么就不再创建该方法。简而言之，该方法使用标志（_initialized）来判断是否已给原型赋予了任何方法。该方法只创建并赋值一次，传统的 OOP 开发者会高兴地发现，这段代码看起来更像其他语言中的类定义了。

#### **重定义已有方法**

![27](E:\Picture\javascript\27.png)

在这段代码中，第一行代码把对当前 toString() 方法的引用保存在属性 originalToString 中。然后用定制的方法覆盖了 toString() 方法。新方法将检查该函数源代码的长度是否大于 100。如果是，就返回错误信息，说明该函数代码太长，否则调用 originalToString() 方法，返回函数的源代码。

![28](E:\Picture\javascript\28.png)

#### 对象冒充

![29](E:\Picture\javascript\29.png)

![30](E:\Picture\javascript\30.png)

![31](E:\Picture\javascript\31.png)

![32](E:\Picture\javascript\32.png)

![33](E:\Picture\javascript\33.png)

### 8 w3school 学习笔记

#### JavaScript：改变 HTML 图像

```html
<!DOCTYPE html>
<html>
<body>
<script>
function changeImage()
{
element=document.getElementById('myimage')
if (element.src.match("bulbon"))
  {
  element.src="/i/eg_bulboff.gif";
  }
else
  {
  element.src="/i/eg_bulbon.gif";
  }
}
</script>

<img id="myimage" onclick="changeImage()" src="/i/eg_bulboff.gif">

<p>点击灯泡来点亮或熄灭这盏灯</p>

</body>
</html>
```

![6](E:\Picture\javascript\6.png)

![7](E:\Picture\javascript\7.png)

![8](E:\Picture\javascript\8.png)

![9](E:\Picture\javascript\9.png)

![10](E:\Picture\javascript\10.png)

![11](E:\Picture\javascript\11.png)

![12](E:\Picture\javascript\12.png)

![13](E:\Picture\javascript\13.png)

![14](E:\Picture\javascript\14.png)

### 9 JavaScript HTML DOM

通过可编程的对象模型，JavaScript 获得了足够的能力来创建动态的 HTML。

- JavaScript 能够改变页面中的所有 HTML 元素
- JavaScript 能够改变页面中的所有 HTML 属性
- JavaScript 能够改变页面中的所有 CSS 样式
- JavaScript 能够对页面中的所有事件做出反应

#### 查找 HTML 元素

通常，通过 JavaScript，您需要操作 HTML 元素。

为了做到这件事情，您必须首先找到该元素。有三种方法来做这件事：

- 通过 id 找到 HTML 元素
- 通过标签名找到 HTML 元素
- 通过类名找到 HTML 元素

![15](E:\Picture\javascript\15.png)

![16](E:\Picture\javascript\16.png)

## Reference

1. [JavaScript教程](http://www.w3school.com.cn/js/index.asp)
2. [定义类或对象](http://www.w3school.com.cn/js/pro_js_object_defining.asp)
3. [继承](http://www.w3school.com.cn/js/pro_js_inheritance_implementing.asp)