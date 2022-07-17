# 原型与原型链

>js中所有的引用类型都有一个`__proto__`属性，该属性值指向了它的构造函数的显式原型prototype属性，当访问一个对象属性时，如果这个对象自身没有该属性，那么就会去他的隐式原型指向的构造函数的prototype对象上去找。prototype本身也是个对象，也有`__proto__`属性，指向了Object。通过原型链和原型对象可以实现继承功能
>
>原型链分为两种，普通对象的原型链和函数对象的原型链
>
>1. 普通对象的原型链，通过new Object或者字面量创建的方式生成的对象，这种对象的原型链比较短，其`__proto__`属性指向了Object的prototype原型对象，Object的prototype原型对象的`__proto__`指向了null，原型链到此结束
>2. 自定义函数的原型链，以下输出全部是true，有两条原型链，实例对象p是通过Person构造函数new出来的，而实例函数Person是通过Function构造函数new出来的
>
>```javascript
>function Person(){
>    
>}
>let p = new Person()
>console.log(p.__proto__ === Person.prototype)
>console.log(Person.prototype.__proto__ === Object.prototype)
>console.log(Person.__proto__ === Function.prototype)
>console.log(Function.prototype.__proto__ === Object.prototype)
>console.log(Object.__proto__ === Function.prototype)
>```

# 作用域与闭包

>作用域决定了程序中定义的变量可以使用的区域，js原生环境提供了两种作用域，全局作用域和函数作用域，但是ES6提供了块级作用域
>
>```javascript
>//1.全局作用域例子
>var a = 1
>function f(){
>    console.log(a)
>}
>f()//1
>//2.函数作用域
>function f(){
>    var a = 1
>}
>console.log(a)//报错
>//3.块级作用域
>if(true){
>    var a = 1
>}
>console.log(a)//1
>if(true){
>    let a = 1
>}
>console.log(a)//报错
>```
>
>js的函数作用域属于词法作用域（静态作用域），其作用域由函数定义时的位置决定，而不是调用时决定
>
>作用域有一个非常重要的使用：模块化
>
>作用域还会生成闭包，闭包定义如下
>
>通过以上例子可以看出，我们在函数外部是无法使用其作用域内部的数据，但是通过返回一个函数对象，就可以使用其内部数据，这就是闭包
>
>```javascript
>// 一个作用域的面试题
>let x = 5;
>function fn(x) {
>    return function(y) {
>        console.log(y + (++x));
>    }
>}
>let f = fn(6);
>f(7);   //14 通过返回的函数引用，使用到了内部的x
>console.log(x); //正常情况下访问到的x是外部的闭包
>```
>
>闭包的一个应用：模拟私有属性
>
>```javascript
>// 模拟私有属性
>function getGeneratorFunc () {
>  var _name = 'John';
>  var _age = 22;
>    
>  return function () {
>    return {
>      getName: function () {return _name;},
>      getAge: function() {return _age;}
>    };
>  };
>}
>var obj = getGeneratorFunc()();
>obj.getName(); // John
>obj.getAge(); // 22
>obj._age; // undefined
>```

# 事件流

>js的事件流包括两个阶段：捕获阶段和冒泡阶段，可以总结为如下的一张图事件捕获由网景提出，事件冒泡由微软提出并分别实现，事件冒泡机制使得事件从内层向外层传播，事件捕获使得事件从外层向内层传播，后来js同时结合了这两种方案，先捕获在冒泡，最底层的元素监听函数的执行顺序根据监听函数代码的先后顺序决定
>
>事件流的应用：事件代理，如果需要监听多个子元素的点击事件，不需要给每个子元素都注册一个监听事件，只需要给父元素注册一个监听事件。
>
>![img](file://E:/work/notebook/52c95304faa114bfedc5665d612a4cc9~tplv-t2oaga2asx-watermark.awebp?lastModify=1648456161)

# 异步Prmoise和async

>ES6中新增了Promise对象用来解决js原来在处理多个异步任务时存在的回调地狱问题，回调地狱是指如果有两个任务a和b，他们都是异步任务，b任务依赖于a任务的返回值，那么原来js的写法是，通过把b任务作为回调函数输入到a的参数，但是随着异步任务的增加，回调任务会越来越多，代码可读性太差
>
>```javascript
>function double(value, success, failure) {
>    setTimeout(() => {
>        try {
>            if (typeof value !== 'number') {
>                throw 'Must provide number'
>            }
>            success(2 * value)
>        } catch (e) {
>            failure(e)
>        }
>    })
>}
>const success = (x) => {
>    double(x, (y) => console.log(`success: ${y}`))
>}
>const failure = (x) => {
>    console.log(`Failure: ${x}`)
>}
>double(3, success, failure)
>```
>
>对于多个异步任务，Promise和async的写法分别如下
>
>```javascript
>Promise.resolve(a)
>  .then(b => {
>    // do something
>  })
>  .then(c => {
>    // do something
>  })
>async () => {
>  const a = await Promise.resolve(a);
>  const b = await Promise.resolve(b);
>  const c = await Promise.resolve(c);
>}
>```
>
>





# ES6 class

> 在ES6之前，js中的对象是通过new构造函数的方式来实现的，这种方法和大多数语言有所区别，而且不方便实现面向对象的一些特性，因此ES6引入了class关键字来实现类。以下两种实现类的方法功能完全一样
>
> ```javascript
> function Point(x, y) {
>   this.x = x;
>   this.y = y;
> }
> 
> Point.prototype.toString = function () {
>   return '(' + this.x + ', ' + this.y + ')';
> };
> 
> var p = new Point(1, 2);
> class Point {
>   constructor(x, y) {
>     this.x = x;
>     this.y = y;
>   }
> 
>   toString() {
>     return '(' + this.x + ', ' + this.y + ')';
>   }
> }
> ```
>
> E6类的所有方法都定义在类的`prototype`上面，所有属性除非定义在this上，否则也是定义在类的`prototype`上
>
> ES6的类和ES5的function不同仅仅在于ES6的类不存在变量提升
>
> ES6类的静态方法，如果在类的方法前加上static关键字，那么该方法不会被实例继承，只能通过`类名.`的方式来调用，静态方法内的this指向具体的实例对象，父类的静态方法可以被子类继承，通过`super`关键字调用
>
> ```javascript
> class Foo {
>   static classMethod() {
>     return 'hello';
>   }
> }
> 
> Foo.classMethod() // 'hello'
> 
> var foo = new Foo();
> foo.classMethod()
> // TypeError: foo.classMethod is not a function
> ```
>
> ES6的class可以使用extends关键字实现继承，如果子类显示定义了`constructor`函数，那么必须在构造函数内通过`super()`显式的调用父类的构造函数，父类的属性会和子类的属性一样，挂在实例对象本身上，而父类的方法会挂在父类的原型对象上，通过原型链进行调用。
>
> ```javascript
> class Point {
>     constructor(x, y) {
>         this.x = x
>         this.y = y
>     }
> 
>     getX() {
>         return this.x
>     }
> 
>     getY() {
>         return this.y
>     }
> }
> 
> class ColorPoint extends Point {
>     constructor(x, y, color) {
>         super(x, y, color)
>         this.color = color
>     }
> 
>     getColor() {
>         return this.color
>     }
> }
> 
> let c = new ColorPoint(1, 2, 'blue')
> // 第一条原型链
> console.log(c.__proto__ === ColorPoint.prototype)
> console.log(ColorPoint.prototype.__proto__ === Point.prototype)
> console.log(Point.prototype.__proto__ === Object.prototype)
> // 第二条原型链
> console.log(ColorPoint.__proto__ === Point)
> console.log(Point.__proto__ === Function.prototype)
> console.log(Function.prototype.__proto__ === Object.prototype)
> ```
>
> ![image-20220328184046379](E:\work\notebook\image-20220328184046379.png)



# 浏览器输入url按下回车的过程

> 1. DNS域名解析（递归解析）
>
> 先查浏览器缓存，再查本地缓存，在查路由器缓存...一直查到根域名服务器
>
> 1. 建立TCP连接（三次握手，四次挥手，为什么三次，为什么四次）
>
> 
>
> 1. 发送http请求（http请求报文格式，请求方式get post等，跨域如何处理，缓存过程）
>
> 
>
> 1. 服务器处理请求并且返回（http响应报文格式，http响应码，缓存设置）
>
> 
>
> 1. 解析http请求，生成渲染页面（重排与重绘）
>
> 解析HTML形成dom树
>
> 解析CSS形成CSSOM树
>
> 合并DOM树和CSSOM树形成渲染树
>
> 浏览器开始渲染页面
>
> ​	

# HTTP+SSL(安全套接层)=https



# 前端的CSRF攻击和XSS攻击



# Vue的响应式实现原理



# 几个设计模式



