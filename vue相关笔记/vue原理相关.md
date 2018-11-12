# 关于vue原理源码笔记

## MVVM

- MVC 数据-视图-控制器

- MVVM 

  1. **前端MVC**：JavaScript可以在前端修改服务器渲染后的数据，Model用js对象表示
  2. View可通过事件触发vm操作，vm可改变数据源，数据层与DOM形成映射关系，数据直接驱动DOM的变化，数据层也可通过vm实现与视图层双向绑定
  3. **双向绑定**：VM负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model
  4. 三层分离，VM操作中并不用关心DOM的结构，只关心数据的存储
  5. model与view绑定能实现：ui的渲染，与ui渲染相关的逻辑

## Vue 如何实现响应式

## Vue 如何解析模板

## Vue 的整个实现流程

## Vue 性能优化相关

## Vue 生命周期

手动执行钩子app.$destroy()销毁

- **beforeCreate**：创建前，new操作，（已绑定事件，还没有数据，不能处理数据 ）

- **create**：创建（可以处理数据）

- **beforeMounted**：挂载前，准备把创建的挂载到el上，有el才去执行挂载（挂载前的el dom仍是<div id="app"></div>）

- 有template转化后执行render funcion再去渲染

  .vue文件中的template是通过vue-loader直接转化直接执行render funcion的减少耗时

- **mounted**：挂载（挂载后$el就是渲染后的<div>123</div>，挂载前后中间执行render funcion）

- **beforeUpdated**：更新前（数据变化）

- **updated**：更新

- **beforeDestroy**：销毁前（组件被销毁，或手动销毁）

- **destroy**：销毁

挂载前的钩子里获取不到el的

render异常：

- renderError(h, err) { return h('div', {}, err.stack)} 
- 只捕获本组件中的render错vue误

## 选项-数据

- **computed**：计算属性，减少计算 ，

  *注：*计算属性内部有get与set方法，在set方法中可做些赋值处理，不支持在计算属性中做赋值处理 

- **watch**：监听到某个变化，执行某个操作，默认只监听引用的变化

  Immediate：true 首次执行一次

  deep：true  深监听一层层遍历，可用'data.name'字符串的方法监听对象下的某个属性

  *注：*计算属性尽量不要修改任何值，watch不要修改监听的那个值