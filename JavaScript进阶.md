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
typeof(undefined) 是undefined；
typeof(null) 是object；

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