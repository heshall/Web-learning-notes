## Array.prototype.slice.call()；

- **slice()** 数组方法，用于切割数组，最终返回一个数组
- **call()** 冒充函数，指定this

把类数组对象变成数组

```javascript
function test(a,b,c,d) { 
  var arg = Array.prototype.slice.call(arguments,1); //arguments表示传进来的值
  return arg;
} 
test("a","b","c","d");	
// b,c,d
```



## 不同数据类型之间的类型转换/隐式转换

### 1. 基本值类型相互转换

- **布尔**
  Boolean()
  true：非空字符串、非零数字、所有对象
  flase：" "、0和NaN、null、undefined

- **数字**

  Number()
  parseInt()
  parseFloat()
  *注：能转换数值的返回NaN*
  isNaN()  //不能转换成数值的返回true，否则返回false

- **字符串**
  toString()

### 2. 引用类型转基本类型

- **Object**
  toString() //返回对象的字符串的表示
  valueOf()  //返回对象的字符串 数值 布尔表示


## json与对象

- **json转对象**：JSON.parse()

- **对象转json**：JSON.stringify()

  ​


## localStorage本地存储值为一个对象

- **JSON.stringify(students)**  //存入前先转化为字符串
- **JSON.parse(students)**  //取出前转化为对象



## js随机数

- Math.random() //返回一个0-1 随机数
- Math.floor(向下取整)

## in操作符

- 判断，对象能够访问某个属性返回true
- hasOwnProperty()，与in能判断属性是在对象中还是在原型中
- for in 返回所有能通过对象访问到的可枚举的属性，不会遍历到原型链上 

## async/await解决异步

**初试**

```javascript
// 字符串识别删除
var reg = new RegExp(tepIndex, 'g')
this.chapterSaveDataId = this.chapterSaveDataId.replace(reg, '')
```

字符串正则替换

```javascript
var tepIndex = 
var reg = new RegExp(tepIndex, 'g')
string.replace(reg,"")

```



