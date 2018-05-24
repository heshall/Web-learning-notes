#**flex** 弹性布局总结笔记

##flex设置

**display:flex/inline-flex**       //是容器成为flex容器
**display:-webkit-flex**           //webkit引擎
***注：使用后float、clear、vertical-align失效***

## 父容器属性：

   

|               属性名 |     属性值     |                 |                  |                    |
| -------------------: | :------------: | :-------------: | :--------------: | :----------------: |
|  **flex-direction:** |    **row**     | **row-reverse** |    **column**    | **column-reverse** |
|       主轴位置文档流 |      左右      |      右左       |       上下       |        下上        |
|       **flex-wrap:** |   **nowrap**   |    **wrap**     | **wrap-reverse** |                    |
| 内容超出flex容器换行 |     不换行     |    向下换行     |     向上换行     |                    |
|       **flex-flow:** | **row nowrap** |                 |                  |                    |
|       以上两种的简写 |     默认值     |                 |                  |                    |



|                 属性名 |   属性值（）   |                |              |                      |                      |
| ---------------------: | :------------: | :------------: | :----------: | :------------------: | :------------------: |
|   **justify-content:** | **flex-start** |  **flex-end**  |  **center**  |  **space-between**   |   **space-around**   |
|               内容布局 |     左对齐     |     右对齐     |     居中     | 两端贴边元素间隔相同 | 两端是元素间隔的一半 |
|       **align-items:** |  **stretch**   | **flex-start** | **flex-end** |      **center**      |     **baseline**     |
| 单行子元素垂直对齐方式 |   高占满容器   |    顶部对齐    |   底部对齐   |       垂直居中       |     文字基线对齐     |
|     **align-content:** |  **stretch**   | **flex-start** | **flex-end** |  **space-between**   |   **space-around**   |
| 多行子元素垂直对齐方式 |    同第一行    |                |              |                      |                      |



##子元素属性

​    1.**order**:<number>    		//当前元素的排列顺序越小越靠前
    2.**flex-grow**：<number>    	//默认0有多余空间也不占用，若都为1剩余空间元素等分，若为2此元素等分比例是其他的一倍
    3.**flex-shrink**: <number> 	//默认为1空间不都自动缩小，若有子元素设0则此元素不缩放
    4.**flex-basis**: 100px | auto  	//auto为元素原宽？
    5.**flex**：0 1 auto(默认)     	//2、3、4的集合   快捷值：auto (1 1 auto) 和 none(0 0 auto)

​    6.**align-self**: auto | flex-start | flex-end | center | baseline | stretch;
        独立：可覆盖容器，单个子元素的align-items垂直对齐方式













