## 父组件——>预览子组件传值

- TalSourceType	     来源类型/ constant.js，SourceType
- TalSourceNameList     来源中l的名字/ vuex，SOURCE_GETTERS_SOURCE_NAME
- TalQuestion                 录题数据：由录入组件callback或者监听一键复制的vuex的变化

## 父组件——>录入子组件传值

- TalQuestion                  录题数据：监听一键复制的vuex的变化

## 封装组件

- 选项：单选，多选，多选多题，判断题，排序题，
- 点击事件onClickxxx

## 字体

```Css
font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
```



## 备忘

- axios拦截器
- nextTick 同步回调
- npm run build —report 打包分析
- dayjs

## ElementUI模块

- 过渡动画
- icon图标

- button按钮
- select下拉框
- switch开关
- rate评分
- tree树形控件
- loading加载
- message消息提示 dialog对话框
- messageBox弹框
- NavMenu导航菜单-侧边栏

## 性能优化

## 

elementUI使用

Tree树形控件：组卷章节弹出选择组件，章节侧面导航展示 

Input输入框：组卷搜索关键字显示学校

Loading加载：组卷相关页面加载、数据请求成功前显示

Popover弹出框：组卷展示来源信息，选择教材版本与年级

Select下拉框：组卷省市区下拉展示，选择学校组件，解决原生select操作繁琐，准备重构来源模块替换原生select

## 章节tree

- 父子半分离，选父不选子，选子要选父
- 选中后只展示父子关系最末级的节点

### 问题

- 选父不选子，选子选父
- 选子后还能不能选父表为同列

### 日志





