# vue 代码规范

> Vue组件化开发
  - 单文件系统，样式局部作用域
  - 基本组成结构：```<template/> <script/> <style scoped/>```
  - 组件注册方式：1）公共组件全局注册 2）其余组件局部注册

### 组件命名规范

Vue官方文档给予以下说明：
>当注册组件 (或者 prop) 时，可以使用 kebab-case (短横线分隔命名)、camelCase (驼峰式命名) 或 PascalCase (单词首字母大写命名)。
PascalCase 是最通用的声明约定而 kebab-case 是最通用的使用约定。

命名可遵循以下规则：
1. 有意义的名词、简短、具有可读性
2. 以小写开头，采用短横线分割命名
3. 公共组件命名以公司名称简拼为命名空间(app-xx.vue)
4. 文件夹命名主要以功能模块代表命名
> 同时还需要注意：必须符合自定义元素规范: 使用连字符分隔单词，切勿使用保留字。app- 前缀作为命名空间: 如果非常通用的话可使用一个单词来命名，这样可以方便于其它项目里复用。  

#### vue文件基本结构

```JavaScript
<template>
    <div>
    <!--必须在div中编写页面-->
    </div>
</template>
<script>
    export default {
    components : {
    },
    data () {
        return {
        }
    },
    methods: {
    },
    mounted() {

    }
    }
</script>
<!--声明语言，并且添加scoped-->
<style lang="less" scoped>
</style>

```

#### vue 方法放置顺序

1. components
2. props
3. data
4. created
5. mounted
6. activited
7. update
8. beforeRouteUpdate
9. metods
10. filter
11. computed
12. watch

#### 注释规范

>代码注释在一个项目的后期维护中显的尤为重要，所以我们要为每一个被复用的组件编写组件使用说明，为组件中每一个方法编写方法说明。

以下情况，务必添加注释
1. 公共组件使用说明
2. 各组件中重要函数或者类说明
3. 复杂的业务逻辑处理说明
4. 特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的hack、使用了某种算法或思路等需要进行注释描述
5. 注释块必须以/\*\*（至少两个星号）开头\*\*/；
    - 组件使用说明，和调用说明 

    ```JavaScript
      <!--公用组件：数据表格
      /**
      * 组件名称
      * @module 组件存放位置
      *@desc 组件描述
      *@author 组件作者
      *@date 2017年12月05日17:22:43
      *@param {Object} [title]    - 参数说明
      *@param {String} [columns] - 参数说明
      *@example 调用示例
     <hbTable :title="title" :columns="columns" :tableData="tableData"></hbTable>
      */
      -->
      ```

6. 单行注释使用//；
    - 普通方法一般使用单行注释// 来说明该方法主要作用

#### 编码规范

优秀的项目源码，即使是多人开发，看代码也如出一人之手。统一的编码规范，可使代码更易于阅读，易于理解，易于维护。``尽量按照ESLint格式要求编写代码``

1. 使用ES6风格编码源码
    - 定义变量使用let ,定义常量使用const
    - 使用export ，import 模块化
2. 组件 props 原子化
    - 提供默认值
    - 使用 type 属性校验类型
    - 使用 props 之前先检查该 prop 是否存在
3. 避免 this.$parent
4. 谨慎使用 this.$refs
5. 无需将 this 赋值给 component 变量
6. 调试信息console.log() debugger 使用完及时删除

#### method 自定义方法命名

1. 动宾短语（good：jumpPage、openCarInfoDialog）（bad：go、nextPage、show、open、login）

2. ajax 方法以 get、post 开头，以 data 结尾（good：getListData、postFormData）（bad：takeData、confirmData、getList、postForm）

3. 事件方法以 on 开头（onTypeChange、onUsernameInput）

4. init、refresh 单词除外

5. 尽量使用常用单词开头（set、get、open、close、jump）

6. 驼峰命名（good: getListData）（bad: get_list_data、getlistData）

#### data props 方法注意点

1. 使用 data 里的变量时请先在 data 里面初始化

2. props 指定类型，也就是 type

3. props 改变父组件数据 基础类型用 $emit ，复杂类型直接改

4. ajax 请求数据用上 isLoading、isError 变量

5. 不命名多余数据，现在是详情页、你的数据是 ajax 请求的，那就直接声明一个对象叫 d，而不是每个字段都声明

6. 表单数据包裹一层 form

#### 生命周期方法注意点

1. 不在 mounted、created 之类的方法写逻辑，取 ajax 数据，可以在 mounted 写一个 getData 方法，去取接口数据，那样这个接口可以复用
2. 在 created 里面监听 Bus 事件

## vue 开发 -- axios

#### axios 挂载

- 改写原型链

> 由于axios 并不能 use()引入，只能每个需要发送请求的组件中即时引入，所以在 main.js 中引入 axios

```JavaScript
import axios from 'axios'
Vue.prototype.$ajax = axios
```

> 添加了这两行代码之后，就能直接在组件的 methods 中使用 $ajax 命令

```JavaScript
methods: {
  submitForm () {
    this.$ajax({
      method: 'post',
      url: '/user',
      data: {
        name: 'wise',
        info: 'wrong'
      }
   })
}
```

#### axios 封装

> 在main.js 中加入

```JavaScript
const get =  (url,params)=>{
  return new Promise((resolve, reject) => {
    axios.get(url, {params:params})
      .then(function (response) {
        resolve(response.data);
      }).catch(err=>{})
  })
};
const post = (url,params)=>{
  return new Promise((resolve, reject) => {
    axios.post(url, params)
      .then(function (response) {
        resolve(response.data)
      }).catch(err=>{})
  })
};

Vue.prototype.$api = api;
Vue.prototype.$get = get;
Vue.prototype.$post = post;

```

在 .vue 页面可以直接使用 this.$get(url,params).then() 和 this.$post(url,params).then()
不需要再加 catch,如果需要特殊参数的请求 可以直接调用 this.axios.get();
使用 this.axios 时必须加上 catch

## vue 开发 -- vuex

1. ajax 判断

> 首先 ajax 请求可以写在 actions也可以直接写在 .vue 页面里;

我们判断的依据是 回调是否需要调用页面结构来区分,
比如在 .vue 页面中 发送完请求后需要调用 this.$refs.element等,或者需要利用组件的独立性的效果时 的那就写在.vue页面,否则就写在 actions 里

2. ajax 调用

```JavaScript
因为异步的原因,不能将 get,post挂载到 vuex 上面,
所以新增 fetch.js 页面:
import axios from 'axios'
import api from './index.js'//api页面
const get =  (url,params)=>{
  return new Promise((resolve, reject) => {
    axios.get(url, {params:params})
      .then(function (response) {
        resolve(response.data);
      }).catch(err=>{})
  })
};
const post = (url,params)=>{
  return new Promise((resolve, reject) => {
    axios.post(url, params)
      .then(function (response) {
        resolve(response.data)
      }).catch(err=>{})
  })
};
export {api,get,post};

在 vuex 页面中引入:import {api,get} from '@/api/fetch.js'
即可发起请求:
    getUser({commit}){
        get(api.info).then(data=>{
          commit('changeUser',data)
        })
    }
    
 如有特殊需要可以新引入 axios 或者在 fetch 上在进行特殊的添加
```

3. 模块

> 按类型分类,将响应模块的state,mutations,actions等分别写在对应文件中,登录,注册,修改密码等写在index 中

4. api管理

  - 新建src/api/index.js
    - 当路径较多时可以再多建几个文件,分类放置
  - 挂载
    - 在 main.js 里 import api from './api/index'
    - 使用 Vue.prototype.$api = api 挂载到原型链上
    - 在 Vuex 里引入有 fetch页面了,这个页面已经将 api 引入了

即使已经在 main.js 中引入了 axios，并改写了原型链，也无法在vuex 的  store.js 中直接使用 $ajax 命令
换言之，这两种方案是相互独立的
在组件中发送请求的时候，需要使用 this.$store.dispatch 来分发

## vuex 的dispatch和commit提交mutation的区别

- 一个异步操作与同步操作的区别。
- 当操作行为中含有异步操作，比如向后台发送请求获取数据，就需要使用action的 dispatch去完成了。
- 其他使用commit即可。
- commit=>mutations,用来触发同步操作的方法。
- dispatch =>actions,用来触发异步操作的方法。

> ---

# vuex 基本使用总结

## 使用

- 在 Vue 的单页面应用中使用，需要使用Vue.use(Vuex)调用插件。
- 使用非常简单，只需要将其注入到Vue根实例中。

```JavaScript
mport Vuex from 'vuex'
Vue.use(Vuex)
const store = new Vuex.Store({
  state: {
    count: 0
  },
getter: {
    doneTodos: (state, getters) => {
      return state.todos.filter(todo => todo.done)
    }
  },
  mutations: {
    increment (state, payload) {
      state.count++
    }
  },
actions: {
  addCount(context) {
    // 可以包含异步操作
    // context 是一个与 store 实例具有相同方法和属性的 context 对象
  }
}
})
// 注入到根实例
new Vue({
  el: '#app',
  store,
  template: '<App/>',
  components: { App }
})
```

然后改变状态：

```JavaScript
this.$store.commit('increment')
```

> Vuex 主要有四部分：

1. state：包含了store中存储的各个状态。
2. getter: 类似于 Vue 中的计算属性，根据其他 getter 或 state 计算返回值。
3. mutation: 一组方法，是改变store中状态的执行者。
4. action: 一组方法，其中可以含有异步操作。

## state 使用

Vuex 使用 state来存储应用中需要共享的状态。为了能让 Vue 组件在 state更改后也随着更改，需要基于state创建计算属性。

```JavaScript
const Num = {
  template: `<div>{{ num }}</div>`,
  computed: {
    num () {
      return this.$store.state.num 
    }
  }
}
```

## getters 使用

类似于 Vue 中的 计算属性，可以在所以来的其他 state或者 getter改变后自动改变。每个getter方法接受 state和其他getters作为前两个参数。

```JavaScript
getters: {
    doneTodos: (state, getters) => {
      return state.todos.filter(todo => todo.done)
    }
  }
```

## mutations 使用

前面两个都是状态值本身，mutations才是改变状态的执行者。mutations用于`同步地更改状态`

```JavaScript
mutations: {
  increment (state, n) {
    state.count += n
  }
}
```

其中，第一个参数是state，后面的其他参数是发起mutation时传入的参数。

```JavaScript
this.$store.commit('increment', 10)
```

commit方法的第一个参数是要发起的mutation名称，后面的参数均当做额外数据传入mutation定义的方法中。

> 规范的发起mutation的方式如下：

```JavaScript
store.commit({
  type: 'increment',
  amount: 10   //这是额外的参数
})
```

额外的参数会封装进一个对象，作为第二个参数传入mutation定义的方法中。

```JavaScript
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

## actions 使用

想要`异步地更改状态`,需要使用action。action并不直接改变state，而是发起mutation.

```JavaScript
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
```

> 发起action的方法形式和发起mutation一样，只是换了个名字dispatch

```JavaScript
// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

## action处理异步的正确使用方式

想要使用action处理异步工作很简单，只需要将异步操作放到action中执行（如上面代码中的setTimeout）。

> 要想在异步操作完成后继续进行相应的流程操作，有两种方式:

1. action返回一个 promise
    - 而dispatch方法的本质也就是返回相应的action的执行结果。所以dispatch也返回一个promise

    ```JavaScript
        store.dispatch('actionA').then(() => {
        // ...
        })
    ```

2. 利用async/await。代码更加简洁

```JavaScript
// 假设 getData() 和 getOtherData() 返回的是 Promise

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // 等待 actionA 完成
    commit('gotOtherData', await getOtherData())
  }
}
```

## 各个功能与 Vue 组件结合(重点)

将state和getter结合进组件需要使用`计算属性`:

```JavaScript
computed: {
    count () {
      return this.$store.state.count 
      // 或者 return this.$store.getter.count2
    }
  }
```

将mutation和action结合进组件需要在 `methods`中调用this.$store.commit()或者this.$store.commit():

```JavaScript
methods: {
    changeDate () {
        this.$store.commit('change');
    },
    changeDateAsync () {
        this.$store.commit('changeAsync');
    }
}
```

## vuex 的扩展功能

为了简便起见，Vuex 提供了四个方法用来方便的将这些功能结合进组件。
1. mapState
2. mapGetters
3. mapMutations
4. mapActions

```JavaScript
import { mapState, mapGetters, mapMutations, mapActions } from 'vuex'

// ....
computed: {
  localComputed () { /* ... */ },
  ...mapState({
    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    count(state) {
      return state.count + this.localCount
    }
  }),
  ...mapGetters({
    getterCount(state, getters) {
      return state.count + this.localCount
    }
  })
}
methods: {
  ...mapMutations({
       add: 'increment' // 将 `this.add()` 映射为`this.$store.commit('increment')`
    }),
  ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
}
```

> 如果结合进组件之后不想改变名字，可以直接使用`数组`的方式(推荐使用)

```JavaScript
methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
}
```

## module -- 模块化

可以将应用的`store`分割为小模块，每个模块也都拥有所有的东西:`state`, `getters`, `mutations`, `actions`

> 首先创建子模块的文件：

```JavaScript
// initial state
const state = {
  added: [],
  checkoutStatus: null
}
// getters
const getters = {
  checkoutStatus: state => state.checkoutStatus
}
// actions
const actions = {
  checkout ({ commit, state }, products) {
  }
}
// mutations
const mutations = {
  mutation1 (state, { id }) {
  }
}
export default {
  state,
  getters,
  actions,
  mutations
}
```

> 然后在总模块中引入：

```JavaScript
import Vuex from 'vuex'
import products from './modules/products' //引入子模块

Vue.use(Vuex)
export default new Vuex.Store({
  modules: {
    products   // 添加进模块中
  }
})
```
