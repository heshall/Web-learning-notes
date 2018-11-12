# ES6基础语法部分

## 变量

**let**     块内声明，有块级作用域 

**const**   常量声明，声明后不可修改,如果声明的对象可修改属性，不可修改的是其引用指针

## 解构赋值

### 数组解构

​	**let a,b; [a,b]=[1,2]** 	//1,2

​	**[a,...b]=[1,2,3,4,5,]**  //1,[2,3,4,5]   /*.代表本变量对应的数组元素*

​	**[a,,..b]=[1,2,3,4,5,]**  //1,[3,4,5]     /*.,代表一个数组元素

### 对象解构

​	**({a,b,c=1}={a:1,b:2})**    //1,2,3 /*c=1是设置的默认值，如果解构赋值没有给变量赋值则返回undefind

​	*注：如果先将变量赋值声明，则对象解构时要先加上圆括号();*

### 字符串解构

​	**cunst[a,b,c,d,e]='wwenj'**
	使用场景：1.变量的交换不用中间值 2.把某数组中的元素赋给变量不用查找索引

### 对象扩展运算符

​    **"...对象"**

```javascript
function fun(...data){
	console.log(data[0]);
	console.log(data[1]);
}
fun(2,5);	 //2,5
```
​   *注： 参数中 "...对象"，就表示此时不是代表对象而是代表对象的每一项元素*

**应用场景：**把数组的值完全赋给另一个数组而不是引用赋值

```javascript
let arr1=[0,1,2];
let arr2=[...arr1];     //代表把arr1中的每个元素赋值给arr2，而不是把arr1的引用赋值给它
arr2.push(3)
console.log(ar r2)       //0,1,2,3
console.log(arr1)       //0,1,2
```

```javascript
rest运算符:剩余代表
    function fun(first,...data){
    console.log(data)      //1,2,3
}
fun(0,1,2,3);
```

### ES6新增的属性与方法

**字符串模板**：
    1.在``中输入字符用${i}插入变量，可插入html标签
    2.${}中可做简单运算

**字符串语法：**
    b.includes(a);	在b中查找是否有a的字符，有返回true
    b.startsWith(a);	查找开头
    b.endsWith(a);	查找结尾
    b.repeat(10);	把b的字符打印10次，字符串加""

**nember语法：**
    Number.isFinite(1)		//ture 判断是否为数字
    Number.isInteger(1)		//ture 判断是否为整型
    Number.parseInt("1")		//1转换为整型
    Number.parseFloat("1")	//1转换为浮点型
    *最大安全整数

**数组语法：**

Array.from()、Array.of()、arr.find()		//对象-数组/数据-数组/数 组查找

注：对象转换成数组格式：json对象中要有**length:3**，一项
       转换数组把属性名为数字的当成转换后的数组索引插入到数组中，从0开始如果没有剩余的数组空位为undefind

```javascript
1.let arr=Array.from(json);	//[] 值转换成数组
2.console.log(Array.of('1','2'))	//[1,2] 能把像大概数组格式的数据识别转换为数组
3.console.log(arr.find(function(value,index,arr){   //当前元素/当前索引/原型
    return value==3  //迭代遍历查找符合条件的返回，查找到即停止返回查找到的内容 //3
}))
```

**for循环：**循环数组用of循环对象用in

```javascript
let arr=[1,2,3];
for(let item of arr){    //循环数组元素的值
	console.log(item)
}

for(let item of arr.keys()){  //循环数组元素的索引
   console.log(item)
}

for(let [value,val] of arr.entries()){  //数组解构赋值 arr.entries()表示[[0,1],[1,2],[2,3]];
   console.log(value+'-'+val)
}

```

   注：*for循环是把每项‘**数组元素的数组元素**’赋值给数组解构变量，直接赋值就代表把‘数组元素’赋值给数组解构变量*



```javascript
*手动循环：输出历史输出记录的下一个数组元素的值next().value
let list=arr.entries();
console.log(list.next());
console.log('----------------')
console.log(list.next().value);
console.log(list.next().value);
```

**枚举对象属性**:in
for(let item in obj){
    console.log(obj[item])	//循环的是属性名，打印的时属性值
}

**箭头函数：**
    let fun=(a)=>{
        console.log(a)
    };
    ***注：箭头函数不能当构造函数用，没有this***

**对象：**
es5判断： 
	+0===-0 		//true
	NaN===NaN	 //false

es6判断看**字面值**： 
	Object.is(+0,-0) 	//false
	Object.is(NaN,NaN)  //true

合并对象：
    let d=Object.assign(a,b,c)  //把abc三个对象属性合并到一起


## Symbol 新类型

Symbol()新数据类型： 不用new
    let sym=Symbol();

```javascript
let setArr=new Set([1,2,3,4,4]); //数组数据类型：去重
setArr.add("王");		//增加
setArr.clear();			//全部清空
setArr.delete(2);		//删除一项
setArr.has(1)				//true 查找
console.log(setArr.size);//4 数组的长度不能用length，从1开始计算
```

**WeakSet()数据结构**，对象数据类型：去重 *不同内存空间的对象不算重复
    let setArr=new WeakSet(); //声明是不能直接传入对象用add()方法添加
    let a={b:5};
    setArr.add(a);  //delete删除 has查找
    console.log(setArr);

**Map()数据结构:**

```javascript
    let map=new Map();
    let obj={
        name:"王",
        age:18
    };
    
    map.set("my",obj);//添加前一个为key键，第二个obj为value值
    map.set(obj,"my");//同上相反
    console.log(map.get(obj));取出map的键obj对应的值
    has查找 delete删除 clear清空 size长度
```



**Proxy进行预处理:**

 ```javascript
let a={name:"王文健"};
let b={
    get:function(target,key,property){  //在调用属性时执行 /此对象 对象键 *
    	console.log("get");
      return target[key]  //最后执行的是这里返回的结果
       },
    set:function(target,key,value,receiver){ //修改键值时执行 /此对象 对象键 对象值
       console.log(set+${value});  //999
       return target[key]=value    //修改信息传入，这里设置修改后的结果
       }
    };
let pro=new Proxy(a,b);
pro.name=999;
console.log(pro.name);
 ```

**promise对象的使用**

```javascript
new Promise(step1).then(function(){
	return new Promise(step2)
}).then(function(){
  return new Promise(step3)
});
```


严格模式：
    可以在块或者函数内部声明严格模式
    *当作用域中有严格模式时出现解构的默认值会报错


es5编译转换方法：
    npm install -g babel -cli  全局安装babel命令行
    npm indtall --save-dev babel-preset-es2015 babel-cli项目安装语法/babel本地
    cnpm install -g live-server   无刷新





