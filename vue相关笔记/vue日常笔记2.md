## Router

**router-link**

```vue
<!-- 字符串 -->
<router-link to="home">Home</router-link>

<!-- v-bind，就像绑定别的属性一样 -->
<router-link :to="'home'">Home</router-link>

<!-- 同上 -->
<router-link :to="{ path: 'home' }">Home</router-link>

<!-- 命名的路由 跳转到name尾user的路由 -->
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>
```

```javascript
export default[
{
path: '/app/:id',
props: true, //:id可以直接传到子组件，不需要$route获取，prop也能直接传值，或者写函数
component: app,
mame: 'app',
meta: { // 加路由下头部信息
    title: 'this is title',
	description:'jj'
},
children:[
	{
	path: 'test',
	component: app,
	}
]
}
]
```



### 导航守卫

**路由全局钩子**

```javascript
//main.js 路由行为
router.beforeEach((to, from, next) => {
    //开始执行
    if (to.fullPath === '/app') { //在路由跳转之前做判断，更改其跳转到的页面 
        next('/login')
    } else {
        next();
    }
})
router.beforeEach((to, from, next) => {
    //执行
    next()；
})
router.beforeEach((to, from) => {
    //最后执行
})
```

**局部路由钩子**

```javascript
//组件中 路由行为 拿不到this上下文，页面还未执行
beforeRouterEnter(to, from, next) {
    //组件中开始执行
    next();
})
beforeRouterUpdate(to, from, next) {
    //同一组件内更新，例通过路由:id获取数据，每次id变化都可以写逻辑
    next();
})
beforeRouterLeave(to, from, next) {
    //组件路由离开
    next(); // 往下进行就要加next，否则停止
})
```



## VUEX

**State**

- 单一状态树，保存状态
- 计算属性调用：对象展开运算符mapState
  ...mapState({ 'age' })

**Getter**

- 对数据进行更改筛选，store的计算属性，被缓存起来
- 计算属性调用：state为第一个参数
- ...mapGetters([ 'age' ])

**Mutation**

- 更改状态的唯一方式
- state为第一个参数，第二参数最好为对象，**必须是同步函数**，常量代替函数名
- 调用`store.commit('increment')`
- methods中调用…mapMutations({ add: 'increment'  })

**Action**

- Action 提交的是 mutation，而不是直接变更状态
- Action 可以包含任意异步操作
- 参数content，获取state，getter
- 调用…mapActions({ add: 'increment' })

使用

1. 应用层级的状态应该集中到单个 store 对象中。
2. 提交 **mutation** 是更改状态的唯一方法，并且这个过程是同步的。
3. 异步逻辑都应该封装到 **action** 里面。





## vue2.x创建项目

```
vue init webpack my-vue
```

Vue watch深拷贝

```vue
    watch: {
        inputAnswerData: {
            handler: function(newVal, oldVal) {
                console.log('newVal:%o', newVal)
                console.log('1this.optionData:%o', this.optionData)
                this.optionData = newVal.items
                console.log('2this.optionData:%o', this.optionData)
            },
            deep: true
        }
    }
```

## 关于vue父子组件通信

**ref传值**

- 如果ref父向子传递的值是个对象的话，那传过来的只是个对象引用，子组件使用时应注意不要引起父组件数据的修改

### 传值（单向数据流）

- 父向子组件中传递的字符串是静态的可直接传入

- 数字，布尔，对象，数组，即使传递的是静态的也需要v-bind，因为这些是js表达式而不是字符串

- **prop传入的只做初始值使用**：复制到data中使用

- **prop传入的做初始值使用且会变化**：在computed中使用

  *如果传进来的是对象数据的话，传进来的是引用，会改变父组件数据，深拷贝操作*

### 祖先组件与子组件间的通信

- ### [provide / inject](https://cn.vuejs.org/v2/api/#provide-inject)