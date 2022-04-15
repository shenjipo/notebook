# 自我介绍

面试官您好，我叫张书铭，来自杭州电子科技大学的硕士，我最开始接触前端是在大一下学期，当时我舍友在图书馆做勤工俭学，大二期间用css和js进行了小米官网静态页面的复刻以及轮播图的实现。大三期间学校开设了web全栈开发的课程，然后我的学习重心由前端转向了后端，并在大三下学期作为项目组长完成了一个机遇SOA框架的新闻发布系统。

接下来就是我的研究生阶段，我的研究方向是面向周期性较强的电力数据的时间序列预测，主要创新点是利用BiLSTM结合的底层原理，做了一个跳跃周期关注，在正常预测方式的基础上加入了跳跃周期关注，这个跳跃周期关注简单来说就是假设我要预测今天3点的电力负载，那么我应该增加对昨天3点，前天3点，以及之前每天3点左右一段时间数据的关注。

在研一上学期，参加了智能拿地强排规划系统项目，由于分配原因，我再次捡起了前端的开发工作，并且再次激发起了我对前端的兴趣。这个项目主要目的是希望用深度学习的方式在对应的住宅出让地上训练出满足制约条件的楼房排布及规划方案，并可以在canvas画布上进行微调，这个项目师兄负责深度学习的训练，我主要负责前端页面的流程及师兄深度学习结果的可视化，主要收获就是接触了canvas画布，了解了canvas的碰撞检测，还有就是自学Three.js对排布方案进行展示。在研一下学期到研二上学期，我除了在做研究方向相关的试验以外，参加了与直升机研究所合作开发的旋翼噪声预估软件开发系统，该项目主要目的为开发一套对复杂飞行轨迹噪声预测的系统，将之前多个部门的流程集成为web网站。我认为该项目是具有一定的现实意义的，目前民用直升机无法大量投入使用的原因主要就是对，虽然这个项目的目的是预测复杂轨迹的噪声，但是我们可以通过这个系统，在该项目中主要担任了登录、数据上传、数据显示以及声学球的显示页面的编写，在该项目中，使用echarts对傅里叶变换和1/3倍频程后的二维数据进行展示以及3维声学球的展示，并运用之前three.js的知识实现了3d联动的效果。这个项目前端使用react，redux，echarts、three.js，layui。后端使用springboot mysql和redis。

# CSS

伪类和伪元素的区别

伪元素是创建一个新的虚拟元素，这个元素不存在DOM文档中，逻辑中存在，但是不在DOM树中

伪类是给特定的元素添加特殊效果，如hover，

## flex布局

done

### **justify-content**对齐方式，flex-start，flex-end，space-between，space-around，center 

- flex-start（默认值）：左对齐
- flex-end：右对齐
- center： 居中
- space-between：两端对齐，项目之间的间隔都相等。
- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-content多轴线对齐方式，注意这是整体的对齐方式

![image-20220402151008323](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220402151008323.png)

## 浏览器渲染流程

1、将获取到的	HTML 页面解析成DOM树

2、css解析，计算出DOM节点的样式

3、构建渲染树，js对每个可见元素找到适配的css样式规则并应用

4、为每个节点生成图形和位置（重排）

5、为每个节点绘制，填充到图层位图中(重绘)

5、图层作为纹理上传至GPU

6、组合多个图层到页面上并生成最终屏幕图像（图层重组）

## 重绘和重排（回流）

重绘是元素样式的改变不影响它在文档流中的位置

重排是部分或者全部元素的尺寸结构等属性发生改变时，浏览器会重新渲染部分或全部文档的过程



### 如何减少回流？

- 避免多层内联样式
- 避免频繁操作样式
- 先用display:none将它移除文档流，然后多次修改后再取消display
- ⽤ visibility: hidden 代替 display: none
- 对复杂动画使用绝对定位，使它脱离文档流，否则会引起父元素及后续元素频繁重排

## 严格模式

使用"use strict " 开启严格模式，ie10以上支持，旧版本忽略

- 严格模式消除了一些js代码中不合理，不严谨指出，减少了一些怪异行为
- 消除代码运行的不安全之处，保证代码运行的安全

|          | 正常模式                                                     | 严格模式                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 变量规定 | 如果一个变量没有声明就赋值，默认为全局变量                   | 必须声明，然后使用                                           |
| this指向 | 在全局作用域中函数指向window<br />构造函数可以new也不可能不new | 全局作用域下指向undefined<br />构造函数不new会当成普通函数，this指向undefined |
| 函数变化 |                                                              | 函数不能有重名参数                                           |







## 前端安全

### xss攻击---跨站脚本攻击

- ###### 反射型

- ###### 存储型

- ###### DOM型（浏览器端完成，属于前端自身漏洞）


## xss攻击 -- 跨站脚本攻击

攻击类型：反射型，存储型，DOM型（浏览器端完成，属于前端自身漏洞）

预防：

- 针对Cookie劫持，可以设置cookie的http-only属性，禁止脚本获取cookie
- 对用户提交的数据进行检查，过滤掉一些符号，如'<'
- 使用CSP（内容安全策略），建立一个白名单，告诉浏览器那些外部资源可以加载和执行（通常有两种方式开启CSP，一种是设置HTTP首部的Content-Security-Policy，一种是设置meta标签的方式

### CSRF攻击 -- 跨站请求伪造攻击

攻击者引诱受害者进入第三方网站，利用受害者在被攻击网站已经获取的注册凭证（如cookie）绕过后台的用户验证，冒充用户对被攻击网站执行某项操作的目的



网站B发给用户一些攻击性代码，并发出一个请求要求用户访问第三方站点A，浏览器接收到后根据B的要求在用户不知情的情况下携带cookie像A发出请求，A根据用户的cookie信息及权限处理该请求，导致恶意代码被执行

（注意，攻击者不是获取到cookie等信息，只是使用）



预防

- **同源检测：**验证http请求头中的Referer字段，可以确定域名来源； 
- 使用**CSRF Token**进行验证，服务器向用户返回一个随机数token，当网站发起请求时，在请求参数中添加上这个token，操作繁琐，还有就是如果请求经过负载平衡转移到了其他服务器，这个服务器中的session没有保留这个token，就没办法验证了
- **在设置 cookie 属性的时候设置 Samesite 模式为严格模式，限制 cookie 不能作为被第三方使用**



### **中间人攻击**

中间人是指攻击者与通讯的两端创建独立的联系，并且交换其所收到的数据，攻击者可以拦截通话或者插入新的内容



- 截获客户端发送给连接请求
- 服务端向客户端发送公钥，中间人截获，保存下，发送个伪造的公钥
- 客户收到伪造的公钥，生成加密hash发给服务器
- 中间人拿到hash，用自己的私钥解密。用服务器的公钥生成假的加密hash发给服务器
- 服务器用私钥解密获得假秘钥，然后加密传给中间人



## 网络劫持

1、DNS劫持，输入京东强制跳转到淘宝

​			方法：1、修改运营商的本地DNS记录，缓存

​							2、劫持信息，然后价格302跳转的回复

2、HTTP劫持，访问谷歌但一直有贪玩蓝月的广告，由于http明文传输，劫持到html请求之后，可以在你的html数据中插入js（广告）

对于DNS劫持，违法，已经被监管起来。

对于HTTP劫持，最有效的办法就是全站HTTPS。将HTTP加密，使运营商无法获取明文，就无法劫持你的响应内容



## React-Ajax







## 同源策略和跨域机制

所谓的同源是指三个相同

- 协议相同（http://)
- 域名相同
- 端口相同

同源的目的是为了用户信息的安全，防止恶意网站窃取数据，如果没有同源策略，网站容易受到CSRF攻击

![preview](https://pic2.zhimg.com/v2-374b1e27b9a6216ba52055a8d07ef9ad_r.jpg)

需要注意的是，很多人以为同源策略是浏览器不让请求发出去、或者后端拒绝返回数据。实际情况是，请求正常发出，后端接口正常响应，只不过**数据到了浏览器后被丢弃了。**



**同源策略的限制**

如果非同源，以下三种方式将会受到限制

- Cookie、LocalStorage和indexDB无法获取
- DOM无法获得
- Ajax请求在浏览器有跨域限制

虽然限制很有必要，但是对日常的开发带来了不好的影响，



### indexDB    非关系型数据库，键值对存储

indexDB存储是异步的，而localStorage操作是同步的，所以indexDB操作时不需要浏览器等待

对于不常变化的数据做浏览器数据缓存，适用于大量数据的存储，数据量不大的时候可以选择使用localStorage

怎么说，，，，想了一下，键值对的，，，虽然是一维的，但是你可以存对象啊，对象里又有键值对，绝了，成二维的了



浏览器支持跨域，但是若干个标签是支持跨域的，如

- <img src="xxx"/>

- <link href="xxx"/>

- <script src="xxx"/>

这些都是加载静态资源的，我们应该关心如何解决AJAX跨域

## 跨域的方法：

### 为什呢要跨域？

我的接口在一个服务器或者一个端口上，我的页面在另一个服务器或者端口上，前端获取数据就会产生跨域问题。

### 1、JSONP

原理：<script>便签不受同源策略的限制，通过script标签指向同一个需要访问的地址，并在本地提供一个回调函数来处理数据

步骤:

​	1、本地定义一个函数

 	2、通过<script>引入跨域服务器上的一个js文件或者其他调用返回js调用的文件，将本地的函数放进url中

​	3、在被引入的文件里，调用这个函数，跨域服务器数据以json的形式填充到这个hs函数的参数里

**缺点：**只支持GET，只支持跨域http请求，不能解决两个页面之间js调用的问题

### **CORS**

**简单请求**

新版本的XMLHttpRequest对象，可以向不同域名的服务器发出HTTP请求。这叫做["跨域资源共享"]

流程：

- 浏览器发送跨域请求
- 服务器收到一个跨域请求后，在响应头中加入**Access-Control-Allow-Origin**资源权限配置，发送响应
- 浏览器收到响应后，查看是否设置了，如果当前域已经得到授权就将结果返回给js，否则忽略此次响应



jsonp兼容性好，老版本的浏览器也支持，但是只支持get请求，发送的数据量有限

cors需要浏览器支持cors功能才行

**非简单请求**

1、预检请求，是否允许跨域请求

2、发送正式请求

### 反向代理

用一个中间人，在3000端口跑着同样一台小服务器，给这个小服务器传信息，不跨域，小服务器和大服务器交互，不跨域，服务器请求不跨域，同源策略限制的是浏览器。

![image-20220402210741865](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220402210741865.png)

react代理配置方法：

1、配置一个带：

在文件package.json最后面补充一个

“proxy”:http://localhost:5000,所有发给3000的请求就都转发给了5000

2、如果想配置多个代理：

在src下创建一个setupProxy.js，这个文件中要写CommonJS的语法，

脚手架会找到这个文件加到webpack中的文件，webpack都是node写的

这里面配置proxy

**工作原理实质上是利用http-proxy-middleware这个http代理中间件，实现请求转发给其他服务器。**



# 计算机网络

## Cookie、Session

session和cookie弥补了http无状态特性，补充和改良，可用session存储一些操作记录

### Session判断同一会话

客户端请求服务端，服务端会给这次请求开辟一个内存空间存储Session，同时生成一个sessionid，并通过响应头的setCookie把这个id传到客户端，让客户端设置Cookie，客户端会设置一个JSSONID=？？？的Cookie信息

#### Session的缺点----如果负载均衡，另一台服务器里没有对应的session

### cookie用于

1. 会话管理，登录购物车，游戏得分
2. 个性化，主题，偏好
3. 记录和分析用户行为

### 永久cookies和会话cookies

如果设置了Expires(特定时间过期）或者Max-Age（特定时间长度）的话，就是永久性的

如果没有设置，那就是客户端关闭时cookie删除

### Cokkie作用域：path和domian标识了cookie的作用域



## HTTP1.0、1.1、2.0

#### http1.0和http1.1的区别

#### http1.X和http2.0的区别

## HTTP报文

### 请求报文

- 请求行，       请求方法，url字段，http协议版本
- 请求头部       产生请求的浏览器类型，请求的主机名host，允许多个域名同出一个ip（虚拟主机）
- 空行         
- 请求体           post/get所携带的数据

### 响应报文

响应行                协议版本，状态码，原因

响应头				

空行

响应体               服务器相应的数据

## HTTP请求

协议特点：

1. 支持客户/服务器模式
2. 请求常用的方式由GET、HEAD、POST, http协议简单，所以http服务器的程序规模小，因此通信速度很快
3. 灵活，允许任意类型的数据对象，类型由content-type标记
4. **无连接：**无连接的含义是限制每次连接只处理一个请求，优点就是节省传输时间，实现简单。称这种无连接为短连接，对应就有了长连接，解决效率问题，缺点是容易造成资源不释放的问题
5. **无状态：**HTTP协议是无状态协议，无状态是指协议对于事务处理没有记忆能力，缺少状态的话，如果后续处理需要前面的信息，那么它必须重传，会导致每次连接传送的数据量增大，为了解决这个问题，Cookie、Session诞生了

| 支持客户/服务器模式<br />协议简单，服务器程序规模小，通信速度快<br />灵活，允许任意类型的数据对象 |                                                |
| ------------------------------------------------------------ | ---------------------------------------------- |
| 无连接，请求一次，服务器处理完后断开，简单，节约传输时间     | 解决：长链接，解决效率问题，容易造成资源不释放 |
| 无状态，对事物处理没有记忆能力                               | Cookie、Session                                |
|                                                              |                                                |





## GET POST

|                      | get                                                         | post                                                         |
| -------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| 参数                 | get请求参数位于url中<br />不安全，参数长度有限制            | post请求的参数位于request body中                             |
| 点击**回退**或者刷新 | GET 请求在浏览器回退时没有影响                              | 再次提交表达，回退是有害的                                   |
| 缓存                 | get能被缓存。参数保留在历史浏览中                           | 不能缓存，不能保存在历史浏览中                               |
| 请求包               | 只发送一个TCP数据包，浏览器会把请求头和请求数据一并发送出去 | 发送两个TCP数据包。，浏览器会先将请求头发送给服务器，待服务器响应100 continue，浏览器再发送请求数据，服务器响应200 ok(返回数据)。 |

关于请求包：



常见状态码：

1表示信息，2表示成功，3表示重定向，4表示客户端错误，5表示服务端错误



## http请求的格式。报文字段



## TCP三次握手，四次挥手的面试描述



## TCP为什么可靠



## 7层模型



## 5层模型



## HTTPS

![image.png](https://cdn.nlark.com/yuque/0/2021/png/1523111/1626073958444-f9d18eaf-d427-462a-8c6b-6ea2d4aecc2e.png)











React路由的基本原理：

浏览器端的路由并不是真实的网页跳转（和服务器没有交互），而是纯粹的在浏览器端发生的一系列行为，本质上来说前端路由就是：对**url进行改变和监听**，**来让某个dom节点显示对应的视图**

路由分为：hash路由和history路由

hash路由特征是url后面会带着#号，锚点 ，改变用location.hash="/foo"，

用window.addEventListener('hashchange') 这个事件，就可以**监听**到 hash 值的变化。

history路由url和普通路径没有差异 ，，，使用history.pushState这个语法改变，

一般使用window.addEventListener("popstate") 事件只可以监听浏览器的回退与前进，所以React重新实现了 history.push() 和history.listen() 方法。

# React

## 生命周期

**为什么要在ComponentDidMount中使用ajax，是因为防止异步请求阻塞页面渲染，可以先显示个Loading，至少这样可以提高用户的体验感。并且ComponentWillMount马上也要被淘汰了**

constructor中只是对state的初始化

### 挂载阶段

##### constructor

初始化state，为事件处理程序绑定this

##### getDerivedStateFromProps

只有当state需要依赖于props时才需要使用

##### render

每次组件渲染都会触发，在这里面不能调用setState

##### ComponentDidMount（）

当第一次渲染完成后，就到了这个，在这个方法中可以发送aJAX异步请求（防止异步操作阻塞UI）可以定义定时器，可以订阅消息。



### 更新阶段

##### getDerivedStateFromProps

##### shouldComponentUpdate

- 主要用于性能优化(部分更新)
- 唯一用于控制组件重新渲染的生命周期，由于在react中，**setState以后，state发生变化，组件会进入重新渲染的流程，在这里return false可以阻止组件的更新**
- 因为react父组件的重新渲染会导致其所有子组件的重新渲染，这个时候其实我们是不需要所有子组件都跟着重新渲染的，因此**需要在子组件的该生命周期中做判断**

##### render

##### getSnapShotBeforeUpdate

**更新之前获取快照**，**返回值将作为参数**传递给`componetDidUpdate()`）

快照，任何值都可以作为快照

##### ComponentDidUpdate

这里可以拿到prevProps和prevState，即更新前的props和state。

### 卸载阶段

##### componentWillUnmount

​	关闭定时器，取消订阅，

## React的消息订阅/发布（手写）

```
PubSub.publish('订阅名'，data)
this.pub = PubSub.subscribe('订阅名'，(_,data) => this.setState(data))
PubSub.unsubscribe(this.pub)
```

## React hooks

## useFetch

```
import { useState, useEffect } from 'react'

export default function useUsers() {

    const [users, setUsers] = useState([])

    useEffect(() => {
        console.log("mount");
        fetch("https://cnodejs.org/api/v1/topics")
            .then(res => res.json())
            .then(json => {
                setUsers(json.data)
                console.log(json.data)
            })
        return () => {
            console.log("unmount");
        }
    }, [])

    return users
}
```

hooks内部使用Object.is()浅比较比较新旧state是否相等

### useState

- setState返回一个数组，因为返回的是数组，所以可以任意命名。
- 如果修改状态时状态值没有发生改变，就不重新渲染
- hooks中的setState不会将新旧DOM进行合并，而是直接替换

### 减少渲染次数

对于类组件可以使用**pureComponent**（帮助开发者实现了shouldComponentUpdate，浅比较，如果在纯组件中重写了shouldComponentUpdate，那就以shouldComponentUpdate的返回值为准）

#### 对于函数组件，现在可以使用useMemo和useCallback来进行优化

给useMemo和useCallback指定依赖项，依赖项不变就不渲染，依赖项变了就渲染



#### useRef

和React.createRef一样，受控组件和非受控组件用，官方说少用ref，看完那句话之后我就能不用ref的尽量没用





# Redux

是react的一个状态管理库，简化了React中的单向数据流，将状态管理完全从React中抽象出来



## Redux如何工作的

​	使用Redux，组件会分为容器组件和展示组件，容器组件负责和Redux的交互，展示组件只负责使用容器组件给的props进行展示ui或者调用容器组件中传递过来的dispatch方法

主要工作流程就是ui组件dispatch一个action发送给store，store将action转发给reducer

reducer中switch case这个action然后根据action的type，实现对应的操作，将action和当前的state作为参数，计算并返回一个新的state，它不会改变state而是总是返回state

当`Redux`状态更改时，连接到`Redux`的组件将接收新的状态作为`props`。当组件接收到这些`props`时，它将进入更新阶段并重新渲染 UI。



![img](https://pic3.zhimg.com/80/v2-a6a023406da2bec21f07693064225b32_720w.jpg)

### 组件如何与redux进行连接？

**mapStateToProps**：此函数将`state`映射到 `props` 上，**因此只要`state`发生变化，新 state 会重新映射到 `props`。 这是订阅`store`的方式。**

**mapDispatchToProps**：此函数用于将 `action creators` 绑定到你的展示组件的`props` 。



### React-Router-Dom组件

**BrowerRouter和HashRouter**是路由器

**Link** 组件用于应用程序中创建链接，它将在HTML中渲染为锚标记

**NavLink**是突出显示当前活动链接的特殊连接

**switch**不是必需的，但是在组合路由中很好用

**Redirect**用于强制路由重定向







# Promise专项

### Promise.then返回的promise结果

由then中的回调函数决定

如果刨出异常，返回的promise为reject

如果返回非promise，resolve

如果返回一个promise，状态和这个promise一样

### Promise.all

```
function PromiseAll(promises){
	return new Promise((resolve,reject) => {

        var resolvedCounter = 0;
        var promiseNum = promises.length;
        var resolvedVals = new Array[promiseNum];
        for(var i = 0;i<promiseNum;i++)
        {   //使用立即执行函数，多个监听函数对所有promise进行监听
            (function(i)	
                {	//测试Promise[i]是否是resolve，是就加1，不是就return
                    Promise.resolve(promises[i]).then(
                    
                    function(value)
                    {
                        resolvedCounter++;//完成数+1
                        resolvedVals[i] = value;
                        if(resolvedCounter === promiseNum)
                        {
                        	//结果数组返回
                            return resolve(resolvedVals)
                        }
                    },
                    function(reason)
                    {
                    	//如果resolve没成功就reject
                        return reject(reason)
                    })
                    
            })(i)
        }
	})
}
```

### Promise.race

```
function PromiseRace(promises){
	return new Promise((resolve,reject) =>{
		if(!Array.isArray(promises)){
			return reject("参数错误") 
		}
		
		for(var i = 0;i<promises.length;i++)
		{
			(function(i){
				Promise.resolve(promises[i]).then(
					res => resolve(res),
					rej => reject(rej)
				)
			})(i)
		}
		
	})
}
```

这个方法可以做3s前执行成功返回resolve，3s后执行返回reject

```
new Promise(resolvePromise ,Timeout(3s))
```

Promise.then的返回

​	确切的说，then、catch、finally返回的不完全是一个promise，而是哦一个thenable对象

### Promise并发控制



```javascript

```

# 手写算法

### Promise.all

核心思想就是使用for循环，立即执行函数，里面写Promise.resolve，能resolve就++num，不能就return reject()

### promise并发控制

```

```



### 手写AJAX

```javascript
const url = "fuck"
let xhr =  new XMLHttpRequest()
//创建HTTP请求,参数是请求的方法、请求的地址
xhr.open("GET",url,true)

//设置状态监听函数，readyState等于4的时候才算请求成功。
xhr.onreadystatechange = function() {
  if (this.readyState !== 4) return;
  // 当请求成功时
  if (this.status === 200) {
    handle(this.response);
  } else {
    console.error(this.statusText);
  }
};

xhr.onerror = function(){
	console.log("错误")
}

//设置响应的数据类型
xhr.responseType = "json"
//设置请求头信息
xhr.setRequestHeader("Accept","application/json")

//发送HTTP请求
xhr.send(null)
```



### 用Promise封装AJAX

```javascript
function getJson(url)
{
	let promise = new Promise(function(resolve,reject) {
		let xhr = new XMLHttpRequest();
		
		xhr.open("GET",url,true);
		xhr.onreadystatechange = function() {
			if(this.readyState !== 4) return;
			if(this.status === 200)
			{
				resolve(this.response)
			}else{
				reject(new Error(this.statusText))
			}
		}
		
		xhr.onerror = function()
		{
			reject(new Error(this.statusText))
		}
        
        //设置响应的数据类型
		xhr.responseType = "json"
        //设置请求头信息
		xhr.setRquestHeader("Accept","application/type")
		xhr.send(null)
	});
	
    return promise;
}
```



### instanceof

```

```

### new

```

```

### call

```
1、判断调用对象是否为函数
2、判断出入上下文对象是否存在，不存在设为window
3、处理传入的参数，截取参数后的所有参数
4、将函数作为上下文对象的一个属性
5、使用该上下文对象调用这个方法
6、删除刚才新增的属性
7、返回结果

Function.prototype.mycall = function(context){
	if(typeof this !== "function") {
		console.log("type error")
	}
	let args = [...argsments].slice(1);
	context = context || window;
	
	context.fn = this;//this是指这个方法，把这个方法设置为上下文对象的属性
	
	res = context.fn(...args)
	delete context.fn;
	return res;
}
```

### 数组去重

```
new Array(new Set(...arr))

[...new Set(arr)]
```

### 柯里化

```
function add(m,n)
{
	return function(n){
		return m+n;
	}
}
```

数组扁平化

将数字每千分位用逗号隔开



深拷贝

解析URL Params为对象

实现数组的map方法







面经不会的

拖拽事件的api有哪些

HTTP请求的格式

懒加载怎么实现的

git常用命令

http版本

箭头函数和普通函数问输出

手写防抖节流









# 其他，项目类

cookie localstorage sessionstroage 

token放在哪，一般放在localstorage里，不过也可以放cookie中

## 登录方式

项目层面：使用axios拦截器

**作用**：当一个请求发出的时候，会先流过 interceptors 的 request 部分，接着请求会发出，当接受到响应时，会先流过 interceptors 的 response 部分，最后返回。在请求或响应被 then 或 catch 处理前拦截它们。

```
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
     //这里经常搭配token使用
    let token = sessionStorage.getItem("token");
    config.headers.Authorization = token; //将token放到请求头发给服务器
    return config;
}, function (error) {
    // 对请求错误做些什么
    console.log("对请求错误做些什么");
    return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    let token = sessionStorage.getItem("token");
    return response;
}, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
});
```

第一次登录后，获取token并存到sessionStorage里



### Cookie+Session

用户访问，输入密码登录

服务器验证密码，创建sessionid，保存起来

服务器响应这个http请求，并通过set-cookie头信息，将sessionID写入Cookie中



###### Cookie+Session的问题

1、服务器存放大量的sessionid

2、负载均衡的话，需要把sessionid同步到每一台及其上，增加服务器维护成本

3、由于sessionid存放在cookie中。无法避免CSRF攻击



### Token登录

服务端生成一个字符串，作为客户端请求的一个令牌

服务器端将token返回给客户端，由客户端自由保存

##### 特点

token不用存放在服务器端，不会对服务器造成压力

token可以放在前端任何地方，可以不用保存在cookie中，提升了页面的安全性

token下发之后。只要在生效时间之内，就一直有效，如果服务器端想收回此token的权限，并不容易

#### 最常见的token的生成方式------JWT

最常见的 Token 生成方式是使用 JWT（Json Web Token），它是一种简洁的，自包含的方法用于通信双方之间以 JSON 对象的形式安全的传递信息。

JWT主要包含3个部分：header头信息（指定该JWT使用的算法），playload消息体（表明了JWT的意图），signature签名



### SSO单点登录

公司内部搭建一个公共的认证中心，公司下的所有产品登录都可以再认证中心完成

## 懒加载

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/efbcb31418be45eaa848d107b107c4eb~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

图片离文档顶部的高度>可视高度+浏览器滚过scrollTop时设置img的data-src





#### 注意：懒加载和预加载

懒加载是用到了才加载，延迟加载

预加载是指将所需的资源提前请求加载到本地，后面需要用到时直接从缓存取资源



## 防抖与节流

防抖是指被触发n秒内再执行回调，则重新计时，可以用在点击请求事件上



节流规定一个单位时间内，只有一次能生效

​	拖拽，固定时间内只能执行一次，防止超高频触发位置变动

​	动画场景，防止短时间内多次触发动画引起性能问题。

## 断点续传

使用Blob.prototype.slice对大文件进行切片

封装xhr

```
request({
	url,
	method = "post"
	data,
	headers = {},
	requestList
})

{
	return new Promise(resolve => {
	const xhr = new XMLHttpRequest();
	xht.open("post",url)
	Object.keys(headers).forEacha(key => 
		xhr.setRquestHeader(key,headers[key])
		);
		xhr.send(data);
		xhr.onload = e =>{
			resolve({
				data:e.target.response
			});
		}
	})
}
```



#### 上传切片

```
const count = 10;//切成10片

生成文件切片
createFileChunk(file, chunkSize){
	let start = 0;
	while(start < file.size)
	{
		fileChunkList.push({file:file.slice(start,start+size)})
		start += chunkSize;
	}
}

//上传切片



//await所有文件块上传成功后发送get请求，让服务端把文件合并


//暂停功能：把上传文件块的请求放在一个数组中，请求完成的从数组中删除，点击暂停，维护数组


//恢复上传
去服务端查询出已经上传的文件块有哪些，上传这些没有成功的文件块。


```

