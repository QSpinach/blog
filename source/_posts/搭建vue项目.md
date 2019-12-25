# 搭建VUE项目

### 概要

本文档用于总结VUE项目的搭建及使用，基于不同的UI搭建原理其实是一样的。以Vant为例简单概述从项目创建到打包部署过程中需要注意的内容。



### 推荐UI

​		移动端：[vant-ui](https://youzan.github.io/vant/#/zh-CN?_blank)、[cube-ui](https://didi.github.io/cube-ui/#/zh-CN/docs/quick-start?_blank)

​		PC端：[element-ui](https://element.eleme.cn/#/zh-CN/component/installation?_blank)、[iView](https://www.iviewui.com/docs/introduce?_blank)



### 环境

1. [nvm](https://github.com/coreybutler/nvm-windows/releases)(node版本管理工具)
2. npm || yarn （包管理工具，高版本nodejs可能需要手动安装npm）
3. [nodejs](https://nodejs.org/zh-cn/download/releases/)（运行环境）



### 开始

#### 创建项目

以`vant-ui`为例子搭建，使用 Vue 官方提供的脚手架 [Vue Cli 3](https://cli.vuejs.org/zh/) 创建项目

```bash
# 安装 Vue Cli
npm install -g @vue/cli

# 创建一个项目
vue create hello-world

# 创建完成后，可以通过命令打开图形化界面，如下图所示
vue ui

# 通过 npm 安装
npm i vant -S

# 通过 yarn 安装
yarn add vant
```



#### 文件目录

```
│  .env.development
│  .env.production
│  .env.sit
│  .env.uat
│  .eslintrc.js
│  .gitignore
│  babel.config.js
│  Dockerfile
│  nginx.conf
│  package-lock.json
│  package.json
│  README.md
│  vue.config.js
│  yarn.lock
│  
├─public
│  │  favicon.ico
│  │  index.html
│  │  
│  └─svg
│          loading-spin.svg
│          
└─src
    │  App.vue
    │  error.js
    │  main.js
    │  permission.js
    │  vant-ui.js
    │  
    ├─api
    │      index.js
    │      login.js
    │      user.js
    │      
    ├─assets
    │    back.png
    │    login.jpg
    │    logo.png
    │          
    ├─components
    │  └─404
    │          index.vue
    │          
    ├─configs
    │      apiURL.js
    │      errorCode.js
    │      index.js
    │      
    ├─routers
    │  │  index.js
    │  │  
    │  └─modules
    │          default.js
    │          
    ├─stores
    │  │  getters.js
    │  │  index.js
    │  │  
    │  └─modules
    │          permission.js
    │          user.js
    │          
    ├─styles
    │      transition.css
    │      
    ├─utils
    │      auth.js
    │      index.js
    │      request.js
    │      validate.js
    │      
    └─views
        │              
        ├─home
        │      Home.vue
        │      Home2.vue
        │      
        ├─login
        │      Login.vue
        │      
        └─test
               Test.vue
```



#### 添加适配方案

##### Rem 适配

Vant 中的样式默认使用`px`作为单位，如果需要使用`rem`单位，推荐使用以下两个工具：

- [postcss-pxtorem](https://github.com/cuth/postcss-pxtorem) 是一款 postcss 插件，用于将单位转化为 rem

- [lib-flexible](https://github.com/amfe/lib-flexible) 用于设置 rem 基准值

  在vue.config.js中配置即可完成适配
  
  ```js
  css: {
      loaderOptions: {
        postcss: {
          plugins: [
            autoprefixer(),
            pxtorem({
              rootValue: 37.5,
              propList: ['*']
            })
          ]
        }
      }
    },
  ```



#### 开发代理

方便开发对接接口及方便管理使用代理，生产可使用nginx做代理

```js
devServer: {
    // 设置主机地址
    // host: 'localhost',
    // 设置默认端口
    port: 8000,
    // 设置代理
    disableHostCheck: true,
    proxy: {
        '/v2': {
          // 目标 API 地址
          target: 'http://rap2api.taobao.org',
          // 如果要代理 websockets
          ws: true,
          // 将主机标头的原点更改为目标URL
          // changeOrigin: true,
          pathRewrite: {
            '^/v2': '/app/mock'    //代理的路径
          }
        }
    }
  },
```



#### 优化引用三方库

使用webpack-bundle-analyzer可以查看各部分打包后的大小，如果太大需要做特殊引用。

在index.html中引用三方库

```html
<script src="//shadow.elemecdn.com/npm/vue@2.6.10/dist/vue.runtime<%= process.env.NODE_ENV === 'production' ? '.min.js' : '.js' %>" crossorigin="anonymous"></script>
<script src="//shadow.elemecdn.com/npm/vue-router@3.0.3/dist/vue-router<%= process.env.NODE_ENV === 'production' ? '.min.js' : '.js' %>" crossorigin="anonymous"></script>
```

在vue.config.js中配置三方库

```js
configureWebpack: {
    plugins: [
      new BundleAnalyzerPlugin()
      // 其他 plugins ...
    ],
    externals: {
      vue: "window.Vue",
      "vue-router": "window.VueRouter"
      // 其他三方库 ...
    }
  }
```



#### 静态变量及环境变量

根据不同的启动命令获取不同的环境变量值，在package.json中配置运行命令执行不同命令会使用不同文件下定义的变量。例如：.env.development、.env.production、.env.sit、.env.uat文件中，默认yarn dev使用development，yarn build使用production，还可以自己添加sit和uat。

```js
"scripts": {
    "dev": "npm run serve",
    "build": "vue-cli-service build",
    "sit": "vue-cli-service build --mode sit",
    "uat": "vue-cli-service build --mode uat"
  },
```

在.env.development中

```js
NODE_ENV='development'
VUE_APP_CURRENTMODE='development'
VUE_APP_BASEURL='http://127.0.0.1:8001'
```

在.env.production中

```js
NODE_ENV='production'
VUE_APP_CURRENTMODE='production'
VUE_APP_BASEURL='http://127.0.0.1:8002'
```

在代码中的使用变量

```js
const baseUrl = process.env.VUE_APP_BASEURL
```

静态变量定义在指定文件中，使用时即可引用。

```js
/**
 * 配置静态变量
 */
// 路由白名单
const whiteList = [
  '/login', // 登录
  '/404'
]
const baseUrl = process.env.VUE_APP_BASEURL
const imgUrl = baseUrl // 图片服务器地址

export {
  whiteList,
  imgUrl
}
```



#### 工具文件

1. 自定义request.js封装axios作为调用接口工具。

   ```js
   // 返回其他状态吗
   service.defaults.validateStatus = function (status) {
     return status >= 200 && status <= 500
   }
   // 处理请求头
   axios.interceptors.request.use(config => {
     const isToken = (config.headers || {}).isToken === false
     let token =  store.getters.access_token // 可以根据vuex或者storage获取
     if (token && !isToken) {
       config.headers['Authorization'] = 'Bearer ' + token // token
     }
     return config
   }, error => {
     return Promise.reject(error)
   })
   // 处理返回信息
   axios.interceptors.response.use(res => {
     const status = Number(res.status) || 200
     const message = res.data.error_description || errorCode[status] || errorCode['default']
     if (status === 401) {
       // TODO 登出
       return
     }
     if (!(status === 200 || status === 204)) {
       // TODO 提示错误信息
       return Promise.reject(new Error(message))
     }
     return res
   }, error => {
     return Promise.reject(new Error(error))
   })
   ```

   在调用接口时候即可使用request工具

   ```js
   import request from '@/utils/request'
   import { apiUrl } from '@/configs/apiURL'
   const login = apiUrl.login
   
   const LoginByMobile = (data) => {
     return request({
       url: login.doLogin,
       method: 'POST',
       type: 'json',
       data,
     })
   }
   ```

   如果想为了方便管理接口地址，可以将接口地址统一管理

   ```js
   const baseUrl = "/v1" // 代理地址
   const baseUrlMock = "/v2" // mock地址
   const apiUrlFn = (baseUrl) => {
     return {
       login: {
         doLogin: baseUrl + "/app/login", // 登录
         doLogout: baseUrl + "/app/logout" // 登出
       },
       user: {
         getUserInfo: baseUrlMock + "/app/userinfo"
       }
     }
   }
   const apiUrl = apiUrlFn(baseUrl);
   export {
     baseUrl,
     baseUrlMock,
     apiUrl
   }
   ```

   

   

   根据不同状态码提示不同的信息，可以做一个errorCode静态变量对象

   ```js
   export default {
     '401': '当前操作没有权限',
     'default': '系统未知错误,请反馈给管理员'
   }
   ```

2. 自定义validate.js作为数据校验工具

   ```js
   /* 大小写字母*/
   export function validateAlphabets(str) {
     const reg = /^[A-Za-z]+$/
     return reg.test(str)
   }
   /* 小写字母*/
   export function validateLowerCase(str) {
     const reg = /^[a-z]+$/
     return reg.test(str)
   }
   ```

   

3. 自定义auth.js作为存储登录token工具（可以用cookie，sessionStorage，localStorage）

   ```js
   import Cookies from 'js-cookie'
   const TokenKey = 'Token'
   export function getToken() {
     return Cookies.get(TokenKey)
     // return sessionStorage.getItem(TokenKey)
   }
   export function setToken(token) {
     // return Cookies.set(TokenKey, token, {expires: 0.001}) // 过期时间一分多钟
     return Cookies.set(TokenKey, token, {expires: 7}) // 过期时间7天
     // return sessionStorage.setItem(TokenKey, token)
   }
   export function removeToken() {
     return Cookies.remove(TokenKey)
     // return sessionStorage.removeItem(TokenKey)
   }
   ```

4. 自定义其他一些好用的数据处理工具

   ```js
   /**
    * 获取地址栏参数
    */
   export function getUrlParam(name) {
     var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)"); //构造一个含有目标参数的正则表达式对象
     var r = window.location.search.substr(1).match(reg);  //匹配目标参数
     if (r != null) return unescape(r[2]); return null; //返回参数值
   }
   ```



### 登录与微信登录

登录需用到vuex和storage以便存储和获取登录用户信息

在store中定义user

```js
state: {
    user: '',
    name: '',
    token: getToken(),
    roles: [],
  },
actions: {
    LoginByMobile({commit}, userinfo){
       return new Promise((resolve, reject) => {
         login.LoginByMobile(userinfo).then(response => {
           const { code, msg, token } = response.data
           if (code != 0) {
               // TODO 提示登录失败
             reject("登录失败")
             return;
           }
           commit('SET_TOKEN', token)
           commit('SET_NAME', "")
           setToken(token)
           resolve(response)
         }).catch(error => {
           reject(error)
         })
       })
     },
},
// 获取用户信息
    GetUserInfo({ commit, state }) {
        return new Promise((resolve, reject) => {
            resolve();
            userApi.getInfo()
                .then(res => res.data)
                .then(res => {
                const { result, msg, code } = res;
                if (code == 0) {
                    commit('SET_NAME', result.name)
                    commit('SET_ID', result.id)
                    commit('SET_ROLES', result.roles)
                    resolve(res);
                } else {
                    reject('error')
                }
            })
                .catch(error => {
                reject('error')
            })
        })
    },
```

在页面定义登录点击事件调用LoginByMobile即可。登录后获取token存入vuex和storage，再获取用户信息存入vuex。

如果是手机端微信登录需要使用openid（微信用户与公众号之间的唯一标识）登录。这里需用到微信的[jssdk](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html)配合后台接口获取openid。

```js
if (getToken()) { // 验证是否含有token
    /* has token*/
    if (to.path === '/login') {
        next({ path: '/' })
        NProgress.done()
    } else {
        if (store.getters.roles.length === 0) { // 判断当前用户是否已拉取完user_info信息
            store.dispatch('GetUserInfo').then(res => { // 拉取user_info
                const roles = res.result.roles // ['user','admin']
                store.dispatch('GenerateRoutes', { roles }).then(() => { // 根据roles权限生成可访问的路由表
                    router.addRoutes(store.getters.addRouters) // 动态添加可访问路由表
                    next({ ...to, replace: true }) // hack方法 确保addRoutes已完成 ,set the replace: true so the navigation will not leave a history record
                })
            }).catch((err) => {
                store.dispatch('FedLogOut').then(() => {
                    next({ path: '/' })
                })
            })
        } else {
            next()
        }
    }
} else {
    const code = getUrlParam('code')
    const openid = sessionStorage.getItem('openid')
    if (code && !openid) {
        // 获取openid
        login.getUserOpenId({
            code: code
        })
            .then(res => res.data)
            .then(res => {
            if (res.code == 0) {
                sessionStorage.setItem('openid', res.openId)
                if (res.token) {
                    store.dispatch('LoginSetToken', {token: res.token}).then(() => { // 拉取user_info
                        setToken(res.token)
                        next()
                    })
                } else {
                    next(`/login`) // 否则全部重定向到登录页
                    NProgress.done()
                }
            }
        }).catch(err => {
            console.log(err)
        })
    } else {
        if (!openid) {
            window.location.href = `https://open.weixin.qq.com/connect/oauth2/authorize?appid=${AppId}&redirect_uri=http%3a%2f%2xx.xxx.com&response_type=code&scope=snsapi_userinfo&state=STATE#wechat_redirect`
        } else {
            /* has no token*/
            if (whiteList.indexOf(to.path) !== -1) { // 在免登录白名单，直接进入
                next()
            } else {
                next(`/login`) // 否则全部重定向到登录页
                NProgress.done()
            }
        }
    }
}
```



### 权限

#### 路由权限

做路由权限有两种，一种是动态路由，一种是静态路由。动态路由信息完全由后台数据库存储，通过接口去获取数据。静态路由则完全由前端控制，可通过不同角色去过滤路由。

静态路由

```js
/* router.js */
const RouterDefault = [
  {
    path: '/',
    name: 'home1',
    component: () => import('@/views/home/Home.vue'), // 普通用户
    meta: { title: '首页', keepAlive: true, noCache: false, roles: ["user"] },
  }, {
    path: '/',
    name: 'other',
    component: () => import('@/views/a_otherRoles/leader/home/index.vue'), // 其他用户
    meta: { title: '首页', keepAlive: true, noCache: false, roles: ["other"] },
  }
 }
```
过滤函数

```js
/**
 * 递归过滤异步路由表，返回符合用户角色权限的路由表
 * @param routes asyncRouterMap
 * @param roles
 */
function filterAsyncRouter(routes, roles) {
  const res = []
  routes.forEach(route => {
    const tmp = { ...route }
    if (hasPermission(roles, tmp)) {
      if (tmp.children) {
        tmp.children = filterAsyncRouter(tmp.children, roles)
      }
      res.push(tmp)
    }
  })

  return res
}

```
过滤路由并添加到vuex中

```js
GenerateRoutes({ commit }, data) {
      return new Promise(resolve => {
        const { roles } = data
        let accessedRouters
        if (roles.includes('admin')) {
          accessedRouters = asyncRouterMap
        } else {
          accessedRouters = filterAsyncRouter(asyncRouterMap, roles)
        }
        commit('SET_ROUTERS', accessedRouters)
        resolve()
      })
    }
```

如果是通过接口获取的路由信息则可以直接拼接静态路由和动态路由信息，当然获取路由信息需要在登录之后或者刷新页面的时候。

```js

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  scrollBehavior: () => ({ y: 0 }),
  routes: constantRouterMap
})

export const asyncRouterMap = [
  ...RouterDefault,
  { path: '*', redirect: '/404', hidden: true }
]
```



#### 按钮权限

按钮权限可以根据角色在前端判断是否展示；也可以在数据库中存储按钮信息，在按钮上绑定的接口权限，通过接口返回按钮信息，前端判断是否展示。

可以自定义定义指令实现按钮展示

```js
// 检查是否包含按钮
function permissionCheck(code) {
  const permissionList = store.getters.permissions
  const stringCode = code.split('||')
  const menuCode = stringCode[0]
  const buttonCode = stringCode[1]
  let checkFlag = false
  permissionList.some((item, index) => {
    if (item.menuCode == menuCode) {
      if(!!item.permitAll) {
        checkFlag = true
      } else {
        item.roleButtons.some((itemBtn, indexBtn) => {
          if (itemBtn.buttonCode == buttonCode) {
            checkFlag = true
            return true
          }
        })
      }
      return true
    }
  })
  return checkFlag
}

/**
 * @export 自定义指令
 */
export function directive() {
  Vue.directive('permit', {
    bind(el, binding) {
      if(!permissionCheck(binding.value)) {
        el.parentNode && el.parentNode.removeChild(el)
      }
    }
  })
}

```

在vue代码中可以使用`v-permit`

```vue
<el-button class="filter-item"
    v-permit="'ROLE-SETTING||role_create'"
    @click="handleCreate"
    size="small"
    type="primary"
    icon="el-icon-edit">
    添加
</el-button>
```



### 问题

1. vue缓存页面使用

   在路由文件中添加`meta` 

    ```js
    {
        path: 'newslist',
        name: 'NewsList',
        meta: {keepAlive: true},
        component: () => import('@/pages/NewsList')
    }
    ```

    在router-view处添加

    ```vue
    <keep-alive>
        <router-view v-if="$route.meta.keepAlive"></router-view>
    </keep-alive>
    <router-view v-if="!$route.meta.keepAlive"></router-view>
    ```

    这样页面就只会加载一次然后缓存起来，再次访问不回刷新数据。

    如果需要在另一个页面跳转过来刷新数据时，则需要使用`beforeRouteLeave` 关键是设置keepAlive

    ```js
    beforeRouteLeave(to, from, next) {
        // 设置下一个路由meta
        to.meta.keepAlive = false; // 让页面不缓存，重新请求数据
        console.log(to);
        next(); // 跳转页面
    }
    ```

2. 页面刷新vuex被清空

    同一页面，刷新后vuex被清空

    - 试用localstorage存储

    - 重新获取数据

      需要某些数据之前先判断一下数据是否存在，如果不存在重新获取。



3. nextTick适当使用

    > 延迟到下次dom更新循环之后执行延迟回调，在修改数据之后立即执行这个方法，获取最新的DOM。获取更新后的DOM言外之意就是什么操作需要用到了更新后的DOM而不能使用之前的DOM或者使用更新前的DOM或出问题，所以就衍生出了这个获取更新后的DOM的Vue方法。所以放在Vue.nextTick()回调函数中的执行的应该是会对DOM进行操作的 js代码.

    - 你在Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中。

      原因：在执行created时并没有dom渲染，此时进行dom操作无效，将执行dom操作的js代码放入nextTick回调函数中，与其相对应的是mounted钩子函数。

    - 在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的DOM结构的时候，这个操作都应该放进Vue.nextTick()的回调函数中。

      原因：vue是异步执行dom更新，一旦观察到数据变化，vue会开启一个队列，然后把在同一个事件循环 (event loop) 当中观察到数据变化的 watcher 推送进这个队列。如果这个watcher被触发多次，只会被推送到队列一次。这种缓冲行为可以有效的去掉重复数据造成的不必要的计算和DOm操作。而在下一个事件循环时，Vue会清空队列，并进行必要的DOM更新。

    简而言之，等待DOM更新之后再进行操作。



4. 组件之间的调用方式

    父子组件

    - prop向下传递，事件向上传递
    - 子组件添加ref属性，父组件可以获取到子组件的实例，不推荐使用
    - 插槽slot 作用域插槽

    非父子组件

    - 使用状态管理

    - 实例化一个公共vue实例

      必须要有公共的实例（可以是空的），才能使用 `$emit` 获取 `$on` 的数据参数，实现组件通信 



5. 计算属性设置值

    > 计算属性是基于它们的依赖进行缓存的，一旦依赖发生变化，计算属性会重新计算

    通过set方法触发它所依赖的变量，单纯的赋值，在取值的时候不会被改变



6. vue文件中内联样式中有无scoped属性的差别

    - 有scoped只在当前vue文件中可以使用这个样式
    - 无scoped，会影响其他文件



7. v-for v-key

    为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。


8. v-for v-if

    当它们处于同一节点，v-for的优先级比v-if更高。



9. 组件、prop大小写不敏感，事件敏感

    不同于组件和 prop，事件名不存在任何自动化的大小写转换。而是触发的事件名需要完全匹配监听这个事件所用的名称。

    不同于组件和 prop，事件名不会被用作一个 JavaScript 变量名或属性名，所以就没有理由使用 camelCase 或 PascalCase 了。



10. prop值的改变--不是立即

    如果父组件中给子组件传递了一个prop的值，然后调用子组件的方法去获取该值，会发现值没有立即改变。

    - 可以监听值的改变去调用相应子组件的方法
    - 将子组件相关方法的调用放在nextTick里面



11. 对象中某属性值的监听

    普通的`watch`中只能监听到某对象的变化才会调用，当想监听对象以及对象中属性的变化都调用函数时，可以使用`deep:true`

    ```js
    data() {
      return {
        bet: {
          pokerState: 53,
          pokerHistory: 'local'
        }   
        }
    },
    watch: {
      bet: {
        handler(newValue, oldValue) {
          console.log(newValue)
        },
        deep: true
      }
    }
    ```


12. this.$forceUpdate

    强制刷新页面，触发页面重新渲染



13. vue中的beforeRouteUpdate

    在`xxx/detail/123`和`xxx/edit/123`都用了同一个组件，`beforeRouteUpdate`不生效，但是watch `$route`是生效的？

    扩展： 可以考虑在路由定义处使用别名 alias

    官方解释

    ```JavaScript
    beforeRouteUpdate (to, from, next) {
        // 在当前路由改变，但是该组件被复用时调用
        // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
        // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
        // 可以访问组件实例 `this`
      },
    ```





### 简单部署

1. 执行命令前端代码打包，生成dist打包后的文件

   ```bash
   yarn build
   ```

2. 将打包后的文件放至指定目录

3. 配置nginx文件

   ```nginx
   server {
       listen       80;
       listen       [::]:80;
       server_name  localhost;
       location / {
           root    /var/www/html;
           index   index.html index.htm;
           try_files $uri $uri/ /index.html;
       }
       location /v2 {
               proxy_set_header Host rap2api.taobao.org;
               proxy_pass http://rap2api.taobao.org;
       }
   }
   ```

4. 重启nginx



### Docker部署

#### 项目打包部署步骤

1. 编写Dockerfile

   ```dockerfile
   FROM docker-registry.xxx/docker/nginx:1.13.6
   COPY ./dist /var/www/html
   COPY ./nginx.conf /etc/nginx/conf.d/ 
   RUN rm /etc/nginx/conf.d/default.conf
   EXPOSE 80
   CMD ["nginx","-g","daemon off;"]
   ```

   

2. 打包镜像

   ```bash
   docker build -t 镜像名 .
   ```

3. 启动容器

   ```bash
   docker run -it --name 容器名 -p 80:80 镜像||id
   ```

#### docker安装

```bash
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
$ sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
$ sudo yum makecache fast
$ sudo yum -y install docker-ce
$ sudo systemctl start docker
```



#### 查看日志

```sh
docker logs -f -t --since=“2017-05-31” --tail=10 容器
–since : 此参数指定了输出日志开始日期，即只输出指定日期之后的日志。
-f : 查看实时日志
-t : 查看日志产生的日期
-tail=10 : 查看最后的10条日志。
```



####  几个命令

```bash
docker start/stop/restart 容器id #启动暂停重启
docker rm 容器id #删除
docker kill 容器id #杀掉一个运行中的容器。
docker pause/unpause 容器id #暂停/取消暂停
docker create 镜像 // 创建容器但是不运行
docker exec -i -t 容器 /bin/bash #开启一个交互模式的终端
docker rmi <image id> # 移除镜像
docker rmi $(docker images | grep "none" | awk '{print $3}') #移除为none的镜像
docker rm $(docker ps -a | grep "Exited" | awk '{print $1 }') #移除为exited的容器
docker images -a 查看镜像
docker ps -a 查看容器
```