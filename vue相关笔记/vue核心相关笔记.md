# vue相关笔记

## 关于配置

1. 关于vue-cli 静态资源打包后引入的路径问题

   - config/ index.js/文件中build选项改成相对路径 './'
   - build/ utils.js/文件中'vue-style-loader'中加入路径 publicPath:'../../'​


## router

**url传值**

- **/index.js** path:'/index/id'
- `<router-link to='/index/123'>`  this.$router 对象中能获取


## transition动画

- **css**

  ![](D:\实验室学习\学习笔记\Typora\assets/vue动画.png)



![](D:\实验室学习\学习笔记\Typora\assets/vue动画原理2.png)

**动画流程出现：**

- **开始前一帧：**点击出现动画，元素由none变为block，动画开始前一帧，插入`opacity:0`属性 **“1”**，和监听opacity属性变化时间为3s **“2”**
- **动画第二帧：**`opacity:0`，属性 **“1”** 去除，引起**“2”**监听执行时间变化
- **动画最后一帧：**动画结束，去除所有

![](D:\实验室学习\学习笔记\Typora\assets/vue动画原理1.png)

**动画流程消失：**

- **开始前一帧：**点击消失动画，元素由block变为none，动画开始前一帧，只插入监听opacity属性变化时间为3s **“4”**
- **动画第二帧：**插入，**“3”** 属性opacity:0引起 **“2”** 监听执行事件变化
- **动画最后一帧：**动画结束，去除所有

## 组件间通信****

- **父—>子:** 

  ```vue
  <progressBar :percent="percent"></progressBar> //父
  
  export default {	//子
    props: {
      percent: {
        type: Number,
        default: 0
      }
    }
  }
  ```

- **子—>父:** 

  ```vue
  this.$emit("percentChange", percent); //子,自定义事件名，传递参数
  
  <progressBar :percent="percent" @percentChange="percentChange"></progressBar> //接受事件
  ```

  