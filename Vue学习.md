# Vue组件生命周期

>Vue的生命周期包括 `开始创建` `初始化数据` `编译模板` `挂载Dom` `渲染` `更新` `卸载`这些过程
>
>![img](E:\work\notebook\2155778-26e10107aaec1030.png)
>
>`Vue`的各个生命周期应用场景
>
>`created` 异步请求数据
>
>`mounted` 挂载元素dom节点的获取
>
>`updated` 数据更新时需要统一处理的业务逻辑
>
>* 父子组件的生命周期
>
>加载过程 父beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted
>
>子组件更新过程 父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated
>
>父组件更新过程 父 beforeUpdate -> 父 updated
>
>销毁过程 父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed
>
>* 父子组件通信
>
>## props与$emit
>
>`props`
>
>```javascript
>//1.子组件通过props接收父组件传递过来的数据 单向传递，浅拷贝，子组件可以拿到父组件的数据，但是不建议修改，如果修改会影响到父组件中的值，如果一定要修改，可以在子组件内部自定义局部变量，然后进行深拷贝，如果是对象，通过watch进行深度监听原父组件的数据来实现局部变量的响应式。
>//子组件
><div>
>     {{message}}
>     <button @click="fn">子组件按钮</button>
></div>
>props: ['message']
>//父组件
><child :message="parentNumber"></child>
>data() {
>    return {
>        parentNumber: 0
>    }
>},
>//2.异步props传递对象，在echarts封装图表时，通常会在父组件的mounted方法中去请求网络数据，这是一个异步操作，然后把请求回来的数据通过props传递给子组件，我们希望子组件接收到数据之后能够根据数据刷新图标显示，所以我们在子组件的mounted方法中接受了message中的options对象，但是子组件并不会刷新显示，是因为，父组件的mounted是一个异步的方法，子组件mounted方法执行时拿到的数据是在网络请求之前的数据，因此需要使用watch监听数据才能实现自动刷新，如果返回的是一个对象，还要使用深度监听
>//子组件
>props: ['message'],
>watch: {
>    message: {
>        handler(newValue, oldValue) {
>            this.childNumber = newValue.number
>        },
>        deep: true
>    }
>},
>mounted() {
>    this.childNumber = this.message.number
>},
>//父组件
><child :message="message"></child>
>mounted() {
>    setTimeout(() => {
>        this.message.number = 4
>    }, 2000)
>},
>```
>
>`emit`子组件发送数据到父组件，在子组件中通过this.$emit('methodName',val)向父组件发送事件，在父组件中通过@methodName = ''进行接收事件
>
>## $childeren与$parent
>
>```javascript
>//父组件
>this.$children[0].messageA = 'this is new value'
>//子组件
>this.$parent.msg;
>```
>
>`$children` 的值是数组，而`$parent`是个对象
>
>## provide/inject
>
>`provide`/ `inject` 是`vue2.2.0`新增的api, 简单来说就是父组件中通过`provide`来提供变量, 然后再子组件中通过`inject`来注入变量。这里不论子组件嵌套有多深, 只要调用了`inject` 那么就可以注入`provide`中的数据，而`不局限于只能从当前父组件的props属性中回去数据`
>
>注意如果provide的数据是非响应式的，那么inject的数据也是非响应式的
>
>```javascript
>//A组件
><script>
>  import comB from '../components/test/comB.vue'
>  export default {
>    name: "A",
>    provide: {
>      for: "demo"
>    },
>    components:{
>      comB
>    }
>  }
></script>
>//B组件
>import comC from '../components/test/comC.vue'
>  export default {
>    name: "B",
>    inject: ['for'],
>    data() {
>      return {
>        demo: this.for
>      }
>    },
>    components: {
>      comC
>    }
>  }
>//C组件
>export default {
>    name: "C",
>    inject: ['for'],
>    data() {
>      return {
>        demo: this.for
>      }
>    }
>  }
>```
>
>## ref
>
>如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例，可以通过实例直接调用组件的方法或访问数据
>
>```javascript
>//子组件
>// 子组件 A.vue
>export default {
>  data () {
>    return {
>      name: 'Vue.js'
>    }
>  },
>  methods: {
>    sayHello () {
>      console.log('hello')
>    }
>  }
>}
>//父组件
>// 父组件 app.vue
><template>
>  <component-a ref="comA"></component-a>
></template>
><script>
>  export default {
>    mounted () {
>      const comA = this.$refs.comA;//通过获取子组件实例
>      console.log(comA.name);  // 调用子组件属性
>      comA.sayHello();  // 调用子组件方法
>    }
>  }
></script>
>```
>
>## eventBus
>
>`eventBus` 又称为事件总线，在vue中可以使用它来作为沟通桥梁的概念, 就像是所有组件共用相同的事件中心，可以向该中心注册发送事件或接收事件， 所以组件都可以通知其他组件。eventBus也有不方便之处, 当项目较大,就容易造成难以维护的灾难。
>
>```javascript
>//Event-bus.js
>import Vue from 'vue'
>export const EventBus = new Vue()
>//A组件发送信息
>additionHandle() {
>    EventBus.$emit('addition', {
>        num: this.num++
>    })
>}
>//B组件接收信息
>EventBus.$on('addition', param => {
>    this.count += param.num
>})
>```
>
>## Vuex
>
>Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态
>
>通过state来保存数据，getters包装数据，mutations同步更新数据，actions异步更新数据
>
>## localStorage / sessionStorage
>
>基本不用
>
>## $attrs与$listeners
>
>如果有以下两个父子组件,子组件的props负责接收指定的参数，$attrs负责接收绑定在子组件html元素上且未被props接收的参数
>
>```javascript
>//父组件
><child-com1
>    :name="name"
>    :age="age"
>    :gender="gender"
>    :height="height"
>    title="程序员成长指北">
></child-com1>
>//子组件
>props: {
>    name: String // name作为props属性绑定
>},
>created() {
>    console.log(this.$attrs);
>    // { "age": "18", "gender": "女", "height": "158", "title": "程序员成长指北" }
>}
>```
>
>常用于多级父子组件通信或者兄弟组件通信

# Vue响应式原理

>Vue 内部通过 `Object.defineProperty`方法属性拦截的方式，把 `data` 对象里每个数据的读写转化成 `getter`/`setter`，当数据变化时通知视图更新
>
>第一步
>
>使用observe函数对所有的数据进行递归遍历，如果重写每个子属性的setter方法，如果数据发生了变化，就会调用setter方法，在setter方法内通过该数据的watcher对象来更新对应的dom
>
>第二步
>
>使用compile解析模板指令，将模板中的变量替换成对应的数据，并且给每一个数据添加一个watcher对象，用来更新dom。还要注册监听事件，实现dom上的数据变化时，把新的dom上的数据更新到对应的data
>
>第三步
>
>watch对象有一个updata方法，用来更新dom
>
>通过 Observer来监听自己的model数据変化，通过 Compile来解析编译模板指令，最终利用 Watcher搭起 Observer和 Compile之间的通信标梁，达到数据视图双向绑定效果



# Vue虚拟dom

> **虚拟DOM**简而言之就是，用js去按照DOM结构来实现的树形结构对象
>
> **Diff算法是一种对比算法**。对比两者是`旧虚拟DOM和新虚拟DOM`，对比出是哪个`虚拟节点`更改了，找出这个`虚拟节点`，并只更新这个虚拟节点所对应的`真实节点`，而不用更新其他数据没发生改变的节点，实现`精准`地更新真实DOM，进而`提高效率`
>
> 