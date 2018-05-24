##指令：

- v-html="msg"  :写在标签中表示把data中的选定内容加入并按html代码在浏览器中渲染
- v-text="msg"  :只是当做文本内容输出到页面
- v-for="item in Dfor" {{itme}}   :在标签中v-for把data中的数组取出赋给item，输出item即可
  数组渲染--(item,index) in Dfor {{itme+index}} :index为数组item的当前位置索引
  对象渲染--(value,key) in Dfor {{itme+key}}  :key为当前对象value的当前属性名
- v-bind:简写‘:’ 持续监听后面属性变量的变化并实时更新  动态绑定 多用于class变化    写法v-bind:class="aa"
  *注：如果标签内属性是不定的变化的一定加上v-bind
- v-if/v-show:v-show="true"表示判断 区别：show存在于文档流由css控制隐藏，if直接消失
- v-else  :必须紧跟在兄弟if后面  当if为flase时执行
- v-model   表单模型双向绑定，input对象<input v-model="aa">{{aa}}</input>
- is="" ：标签内属性，把当前标签替换为is中的标签名， 跟v-bind一起实时变化组件标签
- 其他指令，直接写入标签内，{{}}
    v-pre   保持标签内容原样输出
    v-cloak 标签渲染完成后才显示

**修饰符**

-  v-model.lazy 延时更新，取焦或enter更新
-  v-model.number 只能更新数字  绑定实例对象变为number类型
- v-model.trim   剪切多余空格  *暂试无效
  其他表单控件 标签内设value属性，再model绑定data对象，选中后value的值会添加到对象中

##事件：

  v-on  ：缩写@  @click=""
  @click.stop   :阻止冒泡 .后面是修饰符
  @keydown.enter/13   :表示按下enter键，可跟键盘码
  自定义事件：子组件触发某方法，父组件监听到，父组件执行一个方法
  注：v-on:click="":标签内函数不加括号

**v-once标签内的属性只渲染一次，不双向绑定**

##动画：

- 需要变化内容代码部分外套<transition name="fade"></transition>

|    属性     |          值          |         说明         |               |
| :---------: | :------------------: | :------------------: | :-----------: |
|    .name    |                      | css名称系统命名前缀  |               |
|    ·mode    | in-out先进后出(默认) | out-in先出后进(推荐) |               |
|    ----     |        -----         |         ----         |     ----      |
| -fade-enter |    -enter-active     |        -leave        | -leave-active |
|  即将进入   |     正在进入过程     |      准备出去前      |  出去过程中   |

  注意：透明度默认为1,css不需要写
       多元素交互过度，如标签元素相互变化，*同标签不能显示过度变化，需要在标签中加key=1/2属性区别两标签

--JS  用transition标签内部的js函数动画钩子，
        @before-enter=""动画进入前
        @enter=""进入中
        @after-enter=""进入后
        @enter-cancelled=""进入打断时，离开动画与之相同leave
      函数写在vue的methods中，每个函数有el参数表示当前动画的元素，
      ** 在enter与leave的函数中有el和done两个参数，done在函数结束后必须调用一遍
      ** $(el).animate({opacity:0.8},{duration:1000,complete:done})自定义函数中done调用这样写表示动画完成后在调用



-------------------------------------------------------------------------------------------------
##JS数据选项：

- **data**：     vue实例的对象 用函数的形式更安全data(){return{vue对象}}
- **methods**：  所有用到的函数  其中的this表示vue实例对象data  注：fun(){}=fun:function(){} 'es6'
- **computed**： 计算属性  用函数返回的形式给计算属性中的变量赋值data，data改变计算属性自动改变
                     与函数调用的区别-不必每次使用都调用一遍
- **watch**：    监听属性  每当监听
                   属性变化时调用watch中的此函数，myval:function(val,oldval){},有两个固定参数代表变化前和变化后
- **components**:引入子组件  把通过inport引入的子组件赋值给本组件中设置的变量标签名

##directive:  自定义指令的扩展


**引入组件**：
  import componentA from './componets/a.vue'把文件夹中的a.vue引入当前文件
  当前js中注册此组件：components:{componentA:componentA},
  HTML渲染:<componentA></componentA>

**插槽**：
  父：<componentA><p slot="hearder">准备插在子组件中的内容</p></componentA>
  子：<slot name="hearder"></slot>
  父中的子组件标签中的HTML代码在子组件中显示，插到子组件中，父组件可通过子组件的name属性来选择特定的插入

**组件间通讯**
  props:父组件通过标签内属性向子组件传递属性，子组件用props接收
  事件触发：子向父传递，子组件触发事件父组件通过自定义事件监听到并执行父组件的事件
  插槽

-----------------------------------------------------------------------------------------------

##生命周期：

​    beforecreated，created   实例前后，data初始化前/后
    beforeMount，mounted     挂载前后，el完成初始化/完成挂载
    beforeUpdate，updated    数据更新前/后
    beforeDestroy，destroy   销毁前/后

-----------------------------------------------------------------------------------------------


vue-cli router:
 routes: [
    {
      path: '/hello',
      name: 'Hello',
      component: Hello,
      children:[
        path: '/hi',
        name: 'hi',
        component: hi,
      ]
    }
 ]
    路由：
      <router-view/>  //路由模板输出
      <router-link to="/hello">首页</router-link>

    子路由传参：
      <router-view/> 
      <router-link :to="{name:'hi1',params:{username:'wang',id:'01'}}">路由1</router-link>
      模板:{{$route.params.username}}
    
    单页多路由： 
      入口<router-view name="left"></router-view>
          <router-view name="right"></router-view>
      index.js: components: {   //要渲染到view中的组件 *注:components要加s多个组件
                  default: HelloWorld,  //渲染到默认router-view
                  left: Hi3,  //渲染到name为left的router-view
                  right: Hi4,
                }
    
    路由的重定向/url传参：
      {
        path: '/gohome',  //跳转到的路由
        redirect:'/hello' //跳转后重定向到/hello页
      }
      {
        path:'/hello/:id/:name' //路径为'/hello'后面两个是传参时的键
        component:hello 
      }
      <router-link to="/hello/01/wang">url传参<router-link/> //点击传参 值
      hello.vue {{$route.params.id}} //跳转组件 通过键名获取值
    
    别名：
      {
        path:'/hello',
        component:hello,
        alias:'wang'    //为组件起一个url路由别名，重定向，与redirect不同url不跳转
      }  
    
    mode/404页面：
       router中mode:'history', //url没有#号
       {path:'*',component:error} //跳转到404
    
    路由钩子函数：
      beforeRouteLeave/beforeRouteEnter 进入/出去路由前
      键值对跟函数：(to,from,next)=>{
        console.log(to) //要进入的组件的信息params name Path等
        console.log(from) //进入前所在组件的信息
        next(); //必写，不写不进入下一个组件
      }
    
    路由导航，前进后退：
      this.$router.go(-1)/this.$router.go(1)  //后退/前进 事件触发
      this.$router.push('/home')  //返回home页































