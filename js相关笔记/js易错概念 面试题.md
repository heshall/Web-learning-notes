##函数表达式和函数声明

- 函数声明方式的**函数声明提升优于普通变量提升** 提升整个函数
- 函数表达式等同于普通变量提升 提升声明

```javascript
cosole.log(a)
a();
var a=3;	//普通变量提升 提升声明
function a(){	//函数声明提升，优于变量提升
    console.log('fun10');	
}   
console.log(a)
a=6;
a();  

//输出
//function a(){	
//    console.log('fun10');	
//}, 
//fun10,
//3
//报错
```

*用函数表达式方式只能提升**变量声明**，执行到赋值后才能调用函数*

## 未来元素绑定事件

解决方法：**事件委托**

## 优化方面

###性能优化

- 代码压缩
- 减少/减小/合并/HTTP请求
- 懒加载，预加载
- 小图片用雪碧图，base64格式
- 按需加载

### 代码优化

- 标签语义化，统一命名规范
- 避免@import，!important，和*通配符，避免行内样式，在head引入css
- ​



## 非标准字体的实现

- css3的@font-face



# VUE

- vue的响应式：**Object.defineProperty** 将data属性代理到vm上

- 如何理解MVVM：后端mvc微创新 M-VM-V

- mvvm/vue三要素：响应式，模板引擎，渲染

- **模板引擎**：

  ​