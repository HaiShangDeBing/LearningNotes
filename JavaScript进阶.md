# 类型和值

## 原始类型

- 数字 : Number
- 字符串 : String
- 布尔值 : Boolean

- null : 空类型
- undefined : 变量未初始化

### null与undefined的区别

```javascript
null 		表示一个对象是“没有值”的值，也就是值为“空”；
undefined 	表示一个变量声明了没有初始化(赋值)；

undefined   不是一个有效的JSON，而null是；
typeof undefined 是undefined；
typeof null 是object；

Javascript 将未赋值的变量默认值设为 undefined；

null == undefined //true
null === undefined //false
```

## 对象类型

- Object:对象（引用）
- Array:数组

## 不可变的原始值和可变的对象引用

JavaScript的原始值（undefined，null，布尔值、数字和字符串）是不可更改的。

```
var s="hello";
s.toUpperCase();//返回HELLO，但并没有改变s的值
```

对象和原始值不同，它们的值是可修改的。

对象的比较并非值的比较：即使两个对象包含同样的属性及相同的值，它们也是不相等的。例如各个索引元素完成相等的两个数组也不一定相等。通常将JavaScript对象称为引用类型，对象值都是引用，对象的比较均是引用的比较，当且仅当它们的引用同一个基对象时，它们才相等。

```javascript
var o = {x:1},p = {x:1};	//
o === p						//false
var a = [], b = [];
a === b						//false
var c = a;
c[0] = 1;
a[0]						//1
a === c						//true
```

## 类型转换

### 隐式转换

```javascript
var a="3.14";
var b=a-2;//输出b等于1.14
var c=a+2;//输出c等于3.142
console.log(!a);//false
console.log(!!a);//true，等价于Boolean()
```

- 对于 “-” 运算符，因为字符串不支持减法运算，所以系统自动将字符串转换成数值，对于包含其他字符的字符的字符串，将转换成NaN。
- 对于 “+” 运算符，优先考虑字符串连接，如果其中一个操作数是字符串或者转换为字符串的对象，另外一个操作数将会转换为字符串。
- 对于 "!" 运算符，它将其操作数转换为布尔值并取反。
- 对于 "==" 、"!="、“<”以及其他关系运算符，也会做对象到原始值的转换，但要出去日期对象的特殊情形。

![type convertion](image/javascript/5.png)

### 显示转换

做显示类型转换最简单的方法就是使用

- Boolean()
- Number()
- String()
- Object()

```javascript
Number("3")		//3
String(false)	//"false"
Boolean([])		//true
Object(3)		//new Number(3)
```

JavaScript 也提供了如下几个函数来执行强制类型转换：

- toString():将布尔值、数值等转换成字符串；
- parseInt():将字符串、布尔值等转换成整数；
- parseFloat():将字符串、布尔值等转换成浮点数；
- valueOf():将对象转换为表示它的原始值；

JavaScript中对象到字符串的转换经过如下这些步骤：

- 如果对象具有toString()方法，则调用这个方法。如果这个方法返回一个原始值，JavaScript就将这个值转换为字符串。
- 如果对象没有toString()方法，或者这个方法并不返回一个原始值，那么JavaScript就会调用valueOf()方法。如果存在这个方法，且返回值是原始值，JavaScript就会将这个值转换为字符串。
- 否则，它将抛出一个类型错误异常。

JavaScript中对象到数字的转换则经过如下这些步骤：

- 如果对象具有valueOf()方法，如果这个方法返回一个原始值，JavaScript就将这个值转换为数字。
- 否则，如果对象具有toString()方法，如果这个方法返回一个原始值，JavaScript就将这个值转换为数字。
- 否则，它将抛出一个类型错误异常。

# 变量

## 变量声明 var 和 let

```javascript
var sum;
var i=0,j=0,k=0;

//重复声明
var str="hello";
var str;	//变量str的值依然是hello

//遗漏
var trueVar=1;
fakeVar=2;	//创建全局对象的一个可删除属性
delete fakeVar;	//true，变量被删除
delete trueVar;	//false，变量并没有被删除
```

let 所声明的变量只在 let 所在的代码块内有效。

```javascript
{
    let a = 10;
    var b = 1;
}

a	//ReferenceError: a is not defined
b	//1
```

var 会发生变量提升现象，即变量可以在声明之前使用，值为 undefined。let 所声明的变量一定要在声明后使用，否则便会报错。

```javascript
console.log(a);	//输出 undefined
var a = 2;

console.log(b);	//ReferenceError
let b = 2;
```

只要块级作用域内存在 let 命令，它所声明的变量就绑定这个区域，不再受外部的影响，只要在声明之前使用这些变量，就会报错。

```javascript
var tmp = 123;
if(true){
    tmp = 'abc';	//ReferenceError
    let tmp;
}

function bar(x=y,y=2){
    return [x,y];
}
bar();	//报错
```

let 不允许在相同作用域内重复声明同一个变量。

```javascript
//报错
function（）｛
	let a = 10;
	var a = 1;
｝
//报错
function（）｛
	let a = 10;
	let a = 1;
｝
```

## 作用域链

每一段JavaScript代码都有一个与之关联的作用域链（scope chain）。这个作用域链是一个对象列表或者链表，这组对象定义了这段代码作用域中的变量。当JavaScript需要查找变量x的值的时候（这个过程叫做变量解析），它会从链中的第一个对象开始查找，如果第一个对象中不存在名为x的属性，JavaScript会继续查找链上的下一个对象。如果第二个对象依然没有名为x的属性，则会继续查找下一个对象，以此类推。如果作用域链上没有任何一个对象包含属性x，那么就认为这段代码的作用域链上不存在x，并最终抛出一个引用错误（ReferenceError）异常。

# 运算符

## “+”运算符

- 如果其中一个操作数是对象，则对象会遵循对象到原始值的转换规则转换为原始类值；
- 在进行了对象到原始值的转换后，如果其中一个操作数是字符串的话，另一个操作数也会转换为字符串，然后进行字符串连接；
- 否则，两个操作数都将转换为数字（或者NaN），然后进行加法操作。

## “>>”带符号右移

右边溢出的位将被忽略，填补在左边的位由原操作数的符号决定，一边保持结果的符号与原操作数一致。如果第一个操作数是正数，移位后用0填补最高位，否则用1填补高位。

## “>>>”无符号右移

左边的高位总是填补0.与原来的操作数符号无关。

```javascript
-1>>4=-1
-1>>>4=0x0fffffff
```

## ”===“严格相等运算符

比较过程没有任何类型转换：

- 如果其中一个值是NaN，或者两个值都是NaN，则它们不相等。可以通过`x!===x`来判断x是否为NaN，只有在x为NaN的时候，这个表达式的值才会为true。
- 如果两个引用值指向同一个对象、数组或函数，则它们是相等的。如果指向不同的对象，则它们是不等的，尽管两个对象具有完全一样的属性。
- 如果两个值为字符串，……两个字符串可能含义完全一样且所显示出的字符也一样，但具有不同编码的16位值（UTF-16）。JavaScript并不对Unicode进行标准化的转换。像这样的字符串通过”===“和”==“的比较结果也不相等。

## ”==“相等运算符

如果两个操作数不是同一类型，那么它会尝试进行一些类型转换，然后进行比较。

## 比较运算符

- 只有数字和字符串才能真正执行比较操作，因此其他操作数都将进行类型转换。
- 如果其中一个操作数（或转换后是）是NaN，那么比较操作符总是返回false。
- ”<=“和”>=“运算符在判断相等的时候，并不依赖于相等运算符和严格相等运算符的比较规则。

## ”in“运算符

它的左操作数是一个字符串或可以转换为字符串，右操作数是一个对象。如果右侧的对象拥有一个名为左操作数的属性名，那么表达式返回true。

```javascript
var point = {x:1,y:1};
"x" in point	//true
"z" in point	//false
"toString" in point		//true，对象继承了toString（）方法

var data = {7,8,9};
"0" in data		//true
1 in data		//true,数字转换为字符串
3 in data		//false，没有索引为3的元素
```

## ”&&“运算符

首先计算左操作数的值，如果计算结果是假值，那么整个表达式的结果一定也是假值，因此”&&“这时简单地返回左操作数的值，而且并不会对右操作数进行计算。

如果左操作数是真值，那么整个表达式的结果则依赖于右操作数的值。”&&“运算符会计算右操作数的值并将其返回作为这个表达式的计算结果。

## eval（）运算符

## delete运算符

## void运算符

# 语句

## switch 语句

JavaScript中的case表达式的值是在运行时计算的，这一点使得JavaScript的switch语句和C、C++和Java中的switch语句有很大区别，并且效率也很低。在C、C++和Java中，case表达式必须为同类型的编译时常量，而且switch语句通常会编译成一个跳转表，这让switch语句执行非常高效。JavaScript中的switch语句可以用于字符串，而且能用不是常量的值说明情况。

```javascript
var BLUE = "blue", RED = "red", GREEN  = "green";

switch (sColor) {
  case BLUE: alert("Blue");
    break;
  case RED: alert("Red");
    break;
  case GREEN: alert("Green");
    break;
  default: alert("Other");
}

//这里，switch 语句用于字符串 sColor，声明 case 使用的是变量 BLUE、RED 和 GREEN，这在JavaScript 中是完全有效的。
```

## for in 循环

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

## with 语句

用于临时扩展作用域链，在严格模式中是禁止使用with语句的，并且在非严格模式下也是不推荐使用with语句的。那些使用with语句的JavaScript代码非常难于优化，并且同没有使用with语句的代码相比，它运行得更慢。

```javascript
//这条语句将object添加到作用域链的顶层，然后执行statement，最后把作用域链恢复到原始状态。
with(object)
{
  statements
}
//比如这样一条语句在代码中多处出现，
document.forms[0].address.value=" ";
//则可以使用with语句将form对象添加至作用域链的顶层
with(document.forms[0])
{
  address.value = " ";
}
//当然，不使用with语句的等价代码可以写成这样
var f = document.forms[0];
f.address.value = " ";
```

可以避免重复书写对象。

## debugger 语句

debugger语句通常什么也不做。然而，当调试程序可用并运行的时候，JavaScript解释器将会以调试模式运行。实际上，这条语句用来产生一个端点。

```javascript
function f(o){
    if(o===undefined) debugger;
}
```

## use strict 语句

使用use strict指令的目的是说明（脚本中或函数中）后续的代码将会解析为严格代码。

# 对象

## 创建对象

### 原始方式

```javascript
var oCar = new Object;
oCar.color = "blue";
oCar.doors = 4;
oCar.mpg = 25;
oCar.showColor = function() {
  alert(this.color);
};
//不过这里有一个问题，就是可能需要创建多个 car 的实例。
```

### 工厂方式

```javascript
function createCar(sColor,iDoors,iMpg) {
  var oTempCar = new Object;
  oTempCar.color = sColor;
  oTempCar.doors = iDoors;
  oTempCar.mpg = iMpg;
  oTempCar.showColor = function() {
    alert(this.color);
  };
  return oTempCar;
}

var oCar1 = createCar("red",4,23);
var oCar2 = createCar("blue",3,25);

oCar1.showColor();		//输出 "red"
oCar2.showColor();		//输出 "blue"
//每次调用函数 createCar()，都要创建新函数 showColor()，意味着每个对象都有自己的 showColor() 版本。而事实上，每个对象都共享同一个函数。
```

### 构造函数方式

```javascript
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.showColor = function() {
    alert(this.color);
  };
}

var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);
//就像工厂函数，构造函数会重复生成函数，为每个对象都创建独立的函数版本。
```

### 原型方式

```javascript
function Car() {
}

Car.prototype.color = "blue";
Car.prototype.doors = 4;
Car.prototype.mpg = 25;
Car.prototype.showColor = function() {
  alert(this.color);
};

var oCar1 = new Car();
var oCar2 = new Car();
//调用 new Car() 时，原型的所有属性都被立即赋予要创建的对象，意味着所有 Car 实例存放的都是指向 showColor() 函数的指针。从语义上讲，所有属性看起来都属于一个对象，因此解决了前面两种方式存在的问题。
//使用这种方式，还能用 instanceof 运算符检查给定变量指向的对象的类型

//使用原型方式，不能通过给构造函数传递参数来初始化属性的值,这意味着必须在对象创建后才能改变属性的默认值。
```

```javascript
//原型方式的问题
function Car() {
}

Car.prototype.color = "blue";
Car.prototype.doors = 4;
Car.prototype.mpg = 25;
Car.prototype.drivers = new Array("Mike","John");
Car.prototype.showColor = function() {
  alert(this.color);
};

var oCar1 = new Car();
var oCar2 = new Car();

oCar1.drivers.push("Bill");

alert(oCar1.drivers);	//输出 "Mike,John,Bill"
alert(oCar2.drivers);	//输出 "Mike,John,Bill"
```

### 混合的构造函数/原型方式

```javascript
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.drivers = new Array("Mike","John");
}

Car.prototype.showColor = function() {
  alert(this.color);
};

var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);

oCar1.drivers.push("Bill");

alert(oCar1.drivers);	//输出 "Mike,John,Bill"
alert(oCar2.drivers);	//输出 "Mike,John"
//用构造函数定义对象的所有非函数属性，用原型方式定义对象的函数属性（方法）。结果是，所有函数都只创建一次，而每个对象都具有自己的对象属性实例。
```

### 动态原型方法

```javascript
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.drivers = new Array("Mike","John");
  
  if (typeof Car._initialized == "undefined") {
    Car.prototype.showColor = function() {
      alert(this.color);
    };
	
    Car._initialized = true;
  }
}
//如果Car._initialized这个值未定义，构造函数将用原型方式继续定义对象的方法，然后把它设置为 true。如果这个值定义了（它的值为 true 时，typeof 的值为 Boolean），那么就不再创建该方法。
```

## 重定义对象已有方法

 Function 的 toString() 方法通常输出的是函数的源代码。覆盖该方法，可以返回另一个字符串（在这个例子中，可以返回 "Function code hidden"）。不过，toString() 指向的原始函数将被无用存储单元回收程序回收，因为它被完全废弃了。没有能够恢复原始函数的方法，所以在覆盖原始方法前，比较安全的做法是存储它的指针，以便以后的使用。有时你甚至可能在新方法中调用原始方法：

```javascript
Function.prototype.originalToString = Function.prototype.toString;

Function.prototype.toString = function() {
  if (this.originalToString().length > 100) {
    return "Function too long to display.";
  } else {
    return this.originalToString();
  }
};
```

## 极晚绑定

从技术上讲，根本不存在极晚绑定。该术语是指能够在对象实例化后再定义它的方法。例如：

```javascript
var o = new Object();

Object.prototype.sayHi = function () {
  alert("hi");
};

o.sayHi();
//不建议使用极晚绑定方法，因为很难对其跟踪和记录。不过，还是应该了解这种可能。
```

## 原型

每一个JavaScript对象（null除外）都和另一个对象相关联。另一个对象就是我们熟知的原型，每一个对象都从原型继承属性。比如通过new Array（）创建的对象的原型就是Array.prototype。

### 原型链

没有原型的对象为数不多，Object.prototype就是其中之一。它不继承任何属性。其他原型对象都是普通对象，普通对象都具有原型。所有的内置构造函数（以及大部分自定义的构造函数）都具有一个继承自Object.prototype的原型。例如，Date对象的属性同时继承自Date.prototype和Object.prototype。这一系列链接的原型对象就是所谓的原型链。

# 数组



# 函数