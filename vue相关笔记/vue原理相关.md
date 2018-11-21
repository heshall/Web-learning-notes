# 关于vue原理源码

![](https://user-gold-cdn.xitu.io/2017/12/19/1606e7eaa2a664e8?imageslim)

## MVVM

- MVC 数据-视图-控制器
- MVVM 

  1. **前端MVC**：JavaScript可以在前端修改服务器渲染后的数据，Model用js对象表示
  2. View可通过事件触发vm操作，vm可改变数据源，数据层与DOM形成映射关系，数据直接驱动DOM的变化，数据层也可通过vm实现与视图层双向绑定
  3. **双向绑定**：VM负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model
  4. 三层分离，VM操作中并不用关心DOM的结构，只关心数据的存储
  5. model与view绑定能实现：ui的渲染，与ui渲染相关的逻辑

## Vue 的整个实现流程

![img](/Users/wangwenjian/Desktop/学习/学习笔记/Typora/Web-learning-notes/assets/vue_init.png)

在 **new Vue()** 之后。 Vue 会调用 `_init` 函数进行初始化，也就是这里的 `init` 过程，它会初始化生命周期、事件、 `props`、 `methods`、 `data`、 `computed` 与 `watch` 等。其中最重要的是通过 `Object.defineProperty` 设置 `setter` 与 `getter` 函数，用来实现「响应式」以及「依赖收集」

- ### VDOM

  - `render function`会被转化成VNode节点，vdom就是一颗已js对象为基础的树，用对象来描述节点，**是对真实dom的抽象**
  - 每次视图更新把新的vndoe与旧的vnode传入patch中比较，经过diff算法比较出差异，最后只需要修改差异部分对应的真实DOM即可

## Vue 如何实现响应式

- **Object.defineProperty()**

  ```javascript
  function defineReactive (obj, key, val) {
      Object.defineProperty(obj, key, {
          enumerable: true,       /* 属性可枚举 */
          configurable: true,     /* 属性可被修改或删除 */
          get: function reactiveGetter () {
              return val;         /* 实际上会依赖收集， */
          },
          set: function reactiveSetter (newVal) {
              // 用diff算法辨别差异，再去把差异部分更新
              if (newVal === val) return;
              cb(newVal);
          }
      });
  }
  ```

- **订阅者Dep**

  ```javascript
  class Dep {
      constructor () {
          /* 用来存放Watcher对象的数组 */
          this.subs = [];
      }
      /* 在subs中添加一个Watcher对象 */
      addSub (sub) {
          this.subs.push(sub);
      }
      /* 通知所有Watcher对象更新视图 */
      notify () {
          this.subs.forEach((sub) => {
              sub.update();
          })
      }
  }
  ```

  1. 用 `addSub` 方法可以在目前的 `Dep` 对象中增加一个 `Watcher` 的订阅操作；
  2. 用 `notify` 方法通知目前 `Dep` 对象的 `subs` 中的所有 `Watcher` 对象触发更新操作。

- **观察者**

  ```javascript
  class Watcher {
      constructor () {
          /* 在new一个Watcher对象时将该对象赋值给Dep.target，在get中会用到 */
          Dep.target = this;
      }
      /* 更新视图的方法 */
      update () {
          console.log("视图更新啦～");
      }
  }
  Dep.target = null;
  ```

  ![](https://user-gold-cdn.xitu.io/2017/12/19/1606edad5ca9e23d?imageslim)

  - 首先在 `observer` 的过程中会注册 `get` 方法，该方法用来进行「依赖收集」。在它的闭包中会有一个 Dep 对象，这个对象用来存放 `Watcher` 对象的实例。
  - 「依赖收集」的过程就是把 `Watcher` 实例存放到对应的 `Dep` 对象中去。get 方法可以让当前的 Watcher 对象（Dep.target）存放到它的 subs 中（addSub）方法
  - 在数据变化时，set 会调用 Dep 对象的 notify 方法通知它内部所有的 Watcher 对象进行视图更新。
  - **`Observer` 是一个类，它的作用是给对象的属性添加 getter 和 setter，用于依赖收集和派发更新**

- ### 依赖收集


## Vue 如何解析模板

- **parse**
  parse 会用正则等方式解析 template 模板中的指令、class、style等数据，形成AST。

- **optimize**
  optimize 的主要作用是标记 static 静态节点，这是 Vue 在编译过程中的一处优化，后面当 update 更新界面时，会有一个 **patch** 的过程， **diff 算法会直接跳过静态节点，从而减少了比较的过程，优化了 patch 的性能**。

- **generate**
  generate 是将 AST 转化成 render function 字符串的过程，得到结果是 render 的字符串以及 staticRenderFns 字符串。

- **render function**

  最后渲染VNode的函数

## 数据状态更新时的差异 diff 及 patch 机制



## Vue 性能优化相关

- **optimize**「优化」

  **经过 optimize 这层的处理，每个节点会加上 static 属性，用来标记是否是静态的。**

- **patch** 的过程实际上是将 VNode 节点进行一层一层的比对，然后将「差异」更新到视图上。那么一些静态节点是不会根据数据变化而产生变化的，这些节点我们没有比对的需求，我们就需要为静态的节点做上一些「标记」，在 patch 的时候我们就可以直接跳过这些被标记的节点的比对，从而达到「优化」的目的。

## Vue 生命周期

- **beforeCreate**：创建前，new操作，（已绑定事件，还没有数据，不能处理数据 ）

- **create**：创建（可以处理数据）

- **beforeMounted**：挂载前，准备把创建的挂载到el上，有el才去执行挂载（挂载前的el dom仍是<div id="app"></div>）

- 有template转化后执行render funcion再去渲染

  .vue文件中的template是通过vue-loader直接转化直接执行render funcion的减少耗时

- **mounted**：挂载（挂载后$el就是渲染后的<div>123</div>，挂载前后中间执行render funcion）

- **beforeUpdated**：更新前（数据变化）

- **updated**：更新  this.$forceUpdate()手动更新

- **beforeDestroy**：销毁前（组件被销毁，或手动销毁）  

- **destroy**：销毁  手动执行钩子app.$destroy()销毁

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