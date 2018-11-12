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







```
import Vue from 'vue'
import Router from 'vue-router'
import request from '@/common/request'
import user from '@/store/modules/user'


/* 登录部分组件 */
// import TalLogin from '@/views/Login/TalLogin'
/* End 登录部分组件 */

/* 导入标签部分组件 */
// import BasicLabel from '@/views/tagManagement/BasicLabel'
// import LabelSystem from '@/views/tagManagement/LabelSystem'
/* End 导入标签部分组件 */

/* 录入平台模块 */
// import DirectEntry from '@/views/Entry/Direct/DirectEntry'
// import ResetPassword from '@/views/User/Password/ResetPassword'
// import SystemWrapper from '@/views/Wrapper/SystemWrapper'
// import Wrapper from '@/views/Wrapper/Wrapper'
// import AuthManagement from '@/views/Authorization/AuthManagement'
// import UserAuthorization from '@/views/Authorization/UserAuthorization'
// import EditAuthorization from '@/views/Authorization/EditAuthorization'
// import Tag from '@/views/Tag/TalTag'
// import UserCenter from '@/views/UserCenter/UserCenter'
/* End 录入平台模块 */

/* 组卷组件部分 */
// import ComposeTemplate from '@/views/Compose/composeChoiceTemplate/ComposeChoiceTemplate'
// import ComposeQuestions from '@/views/Compose/composeChoiceQuestions/ComposeChoiceQuestions'
// import ComposeLayout from '@/views/Compose/composeLayout/ComposeLayout'
/* End 组卷组件部分 */

Vue.use( Router )

const router = new Router( {
    mode: "history",
    routes: [ {
            path: '/',
            redirect: '/login'
        },
        {
            path: '/login',
            name: 'Login',
            component: ( resolve ) => require( [ '@/views/Login/TalLogin' ], resolve )
        },
        {
            path: '/school',
            name: 'School',
            component: ( resolve ) => require( [ '@/views/Wrapper/SystemWrapper' ], resolve )
        },
        {
            path: '/questionEntry',
            name: 'QuestionEntry',
            // component: Wrapper,
            component: ( resolve ) => require( [ '@/views/Wrapper/Wrapper' ], resolve ),
            children: [ {
                path: '/questionEntry/directEntry',
                name: 'DirectEntry',
                // component: DirectEntry
                component: ( resolve ) => require( [ '@/views/Entry/Direct/DirectEntry' ], resolve ),
            } ]
        },
        {
            path: '/composeTemplate',
            name: 'ComposeTemplate',
            // component: ComposeTemplate
            component: ( resolve ) => require( [ '@/views/Compose/composeChoiceTemplate/ComposeChoiceTemplate' ], resolve ),
        },
        {
            path: '/composeQuestions',
            name: 'ComposeQuestions',
            // component: ComposeQuestions
            component: ( resolve ) => require( [ '@/views/Compose/composeChoiceQuestions/ComposeChoiceQuestions' ], resolve ),
        },
        {
            path: '/composeLayout',
            name: 'ComposeLayout',
            // component: ComposeLayout
            component: ( resolve ) => require( [ '@/views/Compose/composeLayout/ComposeLayout' ], resolve ),
        },
        {
            path: '/auth',
            // component: Wrapper,
            component: ( resolve ) => require( [ '@/views/Wrapper/Wrapper' ], resolve ),
            children: [ {
                    path: '/auth/authManagement',
                    name: 'AuthManagement',
                    // component: AuthManagement
                    component: ( resolve ) => require( [ '@/views/Authorization/AuthManagement' ], resolve ),
                },
                {
                    path: '/auth/userAuthorization/:id',
                    name: 'UserAuthorization',
                    // component: UserAuthorization
                    component: ( resolve ) => require( [ '@/views/Authorization/UserAuthorization' ], resolve ),
                },
                {
                    path: '/auth/editAuthorization',
                    name: 'EditAuthorization',
                    // component: EditAuthorization
                    component: ( resolve ) => require( [ '@/views/Authorization/EditAuthorization' ], resolve ),
                }
            ]
        },
        {
            path: '/tag',
            // component: Wrapper,
            component: ( resolve ) => require( [ '@/views/Wrapper/Wrapper' ], resolve ),
            children: [ {
                path: '/tag',
                name: 'Tag',
                // component: Tag
                component: ( resolve ) => require( [ '@/views/Tag/TalTag' ], resolve ),
            } ]
        },
        {
            path: '/center',
            // component: Wrapper,
            component: ( resolve ) => require( [ '@/views/Wrapper/Wrapper' ], resolve ),
            children: [ {
                path: '/center',
                name: 'center',
                // component: UserCenter
                component: ( resolve ) => require( [ '@/views/UserCenter/UserCenter' ], resolve ),
            } ]
        },
        {
            path: '/tagManagement',
            // component: Wrapper,
            component: ( resolve ) => require( [ '@/views/Wrapper/Wrapper' ], resolve ),
            children: [ {
                    path: '/tagManagement/basicLabel',
                    name: 'BasicLabel',
                    // component: BasicLabel
                    component: ( resolve ) => require( [ '@/views/tagManagement/BasicLabel' ], resolve ),
                },
                {
                    path: '/tagManagement/labelSystem',
                    name: 'LabelSystem',
                    component: ( resolve ) => require( [ '@/views/tagManagement/LabelSystem' ], resolve ),
                }
            ]
        },
        {
            path: '/user/rsetPassword',
            name: 'resetPassword',
            component: ( resolve ) => require( [ '@/views/User/Password/ResetPassword' ], resolve ),
        }
    ]
} )

router.beforeEach( ( to, from, next ) => {
    let auth_token = sessionStorage.getItem( 'auth_token' )
    if ( auth_token ) {
        user.state.auth_token = auth_token
        request.request.defaults.headers.Authorization = auth_token
    } else {
        if ( to.name != "Login" ) router.push( {
            name: 'Login'
        } )
    }
    next()
} )

export default router

```

