- **js**
  - 闭包\
  要理解闭包，首先要知道javascript的作用域。通常javascript作用域分为全局作用域和函数内作用域，通常来说一个函数执行开始到结束也意味着一个作用域的创建到销毁，如果函数A内变量被引用，则A会在内存中驻留一段时间直至A内变量都被释放，我们就可以将这个函数作用域称之为闭包。也可以这么说，闭包是函数作用域的一种使用方式的实现。使用闭包会引起内存升高，应尽量规避闭包，使用let替代var是一种非常好的方式。
  - 原型和继承\
  [JavaScript 原型](https://juejin.im/post/5bc755b15188255c89015f39)
    >由于 JS 没有'类', 所以采用了原型的方式实现继承，正确的说法是引用或者委托，因为对象之间的关系不是复制，而是委托。在查找属性的时候，引用（委托）原型对象的属性，也就是我们常说的原型继承。
    
    [JavaScript 继承](https://www.jianshu.com/p/5cb692658704)
    >原型继承
    
    ```
        function Person(name){
         this.name=name;
         this.className="person" 
        }
        Person.prototype.getClassName=function(){
         console.log(this.className)
        }
        
        function Man(){
        }
        
        Man.prototype=new Person();//1
        //Man.prototype=new Person("Davin");//2
        var man=new Man;
        >man.getClassName()
        >"person"
        >man instanceof Person
        >true
    ```

    >构造函数继承
    
    ```
    function Person(name){
     this.name=name;
     this.className="person" 
    }
    Person.prototype.getName=function(){
     console.log(this.name)
    }
    function Man(name){
      Person.apply(this,arguments)
    }
    var man1=new Man("Davin");
    var man2=new Man("Jack");
    >man1.name
    >"Davin"
    >man2.name
    >"Jack"
    >man1.getName() //1 报错
    >man1 instanceof Person
    >true
    
    ```
    
    >组合继承
    
    ```
        function Person(name){
         this.name=name||"default name"; //1
         this.className="person" 
        }
        Person.prototype.getName=function(){
         console.log(this.name)
        }
        function Man(name){
          Person.apply(this,arguments)
        }
        //继承原型
        Man.prototype = new Person();
        var man1=new Man("Davin");
        > man1.name
        >"Davin"
        > man1.getName()
        >"Davin"
    ```
    
    >寄生组合继承
    
    ```
        function Person(name){
         this.name=name; //1
         this.className="person" 
        }
        Person.prototype.getName=function(){
         console.log(this.name)
        }
        function Man(name){
          Person.apply(this,arguments)
        }
        //注意此处
        Man.prototype = Object.create(Person.prototype);
        Man.prototype.constructor = Man;
        var man1=new Man("Davin");
        > man1.name
        >"Davin"
        > man1.getName()
        >"Davin"
    ```
    >ES6继承
    
    ```
    class Person{
          //static sCount=0 //1
          constructor(name){
             this.name=name; 
             this.sCount++;
          }
          //实例方法 //2
          getName(){
           console.log(this.name)
          }
          static sTest(){
            console.log("static method test")
          }
        }
        
        class Man extends Person{
          constructor(name){
            super(name)//3
            this.sex="male"
          }
        }
        var man=new Man("Davin")
        man.getName()
        //man.sTest()
        Man.sTest()//4
        输出结果：
        Davin
        static method test
    ```
    还是用TypeScript吧，强行安利
    [TypeScript](https://www.tslang.cn/),
    再强行安利[angular](https://angular.cn)哈哈
  - 解决回调地狱
  
    [这个讲解很清晰：Promise](https://segmentfault.com/a/1190000009478377?utm_source=tag-newest)

    [async await](https://segmentfault.com/a/1190000013292562?utm_source=channel-newest#articleHeader6)
    
  - this\
  [tihs](https://segmentfault.com/a/1190000017452514)\
  this是Javascript语言的一个关键字。 它代表函数运行时，自动生成的一个内部对象，只能在函数内部使用。随着函数使用场合的不同，this的值会发生变化。但是有一个总的原则，那就是this指的是，调用函数的那个对象
    
  - 深拷贝浅拷贝
  
    深拷贝是递归复制了一个对象的属性和值到另一个对象上\
    浅拷贝相当于对象引用
  - 箭头函数
    
    没找到比较好的中文资料，看MDN吧
     [Arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
    
  - ES6、7
    
    [ES6看这里](http://es6.ruanyifeng.com/)
    
    [ES7看这里](https://www.jianshu.com/p/13c5d002478b)

  - 防抖节流
  
    [看这里](https://mp.weixin.qq.com/s/Vkshf-nEDwo2ODUJhxgzVA)

    **函数防抖**：将几次操作合并为一此操作进行。原理是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，就会取消之前的计时器而重新设置。这样一来，只有最后一次操作能被触发。
    
    **函数节流**：使得一定时间内只触发一次函数。原理是通过判断是否到达一定时间来触发函数。
    
    **区别**： 函数节流不管事件触发有多频繁，都会保证在规定时间内一定会执行一次真正的事件处理函数，而函数防抖只是在最后一次事件后才触发一次函数。 比如在页面的无限加载场景下，我们需要用户在滚动页面时，每隔一段时间发一次 Ajax 请求，而不是在用户停下滚动页面操作时才去请求数据。这样的场景，就适合用节流技术来实现。
- **DOM**
    - 事件冒泡
  
    所谓冒泡就是子元素会将事件传递给父元素，向上传递过程就像冒泡一样。当然这个冒泡事件可以阻止
    ```
      //阻止事件冒泡-标准浏览器
    　e.stopPropagation();
    　
    　//阻止事件冒泡-IE
    　event.cancelBubble = true;
    ```

  - 事件委托
    
    事件委托通常会用在处理动态元素的事件上，利用的原理就是事件冒泡。例如父元素parent的子元素child是动态生成的，如果要监听child元素的事件，可以通过在父元素事件内判断事件源是否是child元素，由此来执行对应的函数。这种方式通常用在以jquery为主的技术栈的项目，如果你使用的是mvvm一类框架，那么使用到事件委托的机会可能会很少
- **BOM**
  - location
  - history
  - Navigator
  - cookie
- **css**
  - 标准盒模型
  - IE盒模型
  - flex布局
  - 垂直居中
  - 水平居中
  - 定位
  - css继承
  - 文本省略号
  - 多行文本省略号
  - 双边距重叠
- **html5**
  - sessionStorage
  - localStorage
  - web worker
  - webscoket
- **css3**
  - 帧动画animation
  - 过渡transition
  - 形变transform
  - 字体@font-face
- **vue**
- **react**
- **webpack**
- **http、https**
  - http和https的区别 
  - get请求的误区
  - get和post的区别
  - 状态码
- **restful** 
- **优化**
  - 减少请求次数\
  合并图片、js、css
  - 缩小请求包体\
  压缩图片、js、css
  - 懒加载\
  对非必须立刻展示的内容，延迟加载或者懒加载（需要时再加载）
  - 预加载\
  将资源提前加载到浏览器备用
  - 缓存\
  首页静态化，redis缓存，网站缓存，CDN缓存，客户端缓存。
- **工程化**  
  - 模块化
  - 标准化
  - 自动化
- **前端安全**
  - XSS跨站攻击\
  XSS指的是攻击者漏洞，向 Web 页面中注入恶意代码，当用户浏览该页之时，注入的代码会被执行，从而达到攻击的特殊目的。
  - http劫持
  - DNS劫持
  - HTTPS 与 CSP\
  CSP 即是 Content Security Policy，翻译为内容安全策略。这个规范与内容安全有关，主要是用来定义页面可以加载哪些资源，减少 XSS 的发生。\
  能够实施 HTTP 劫持的根本原因，是 HTTP 协议没有办法对通信对方的身份进行校验以及对数据完整性进行校验。如果能解决这个问题，则劫持将无法轻易发生。\
  HTTPS，是 HTTP over SSL 的意思。SSL 协议是 Netscape 在 1995 年首次提出的用于解决传输层安全问题的网络协议，其核心是基于公钥密码学理论实现了对服务器身份认证、数据的私密性保护以及对数据完整性的校验等功能。


- promise与fetch区别
- react组件的生命周期
- UI组件与容器组件
- redux/vuex
- 前端性能优化
- 浏览器存储原理
- webpack配置
- react路由/vue-router
- promise跨域
- vue双向绑定原理
- vue和react的区别
- 对原型链的理解？prototype上都有哪些属性
- 为什么使用继承
- jQuery addClass()的内部实现
- jQuery的优缺点，与vue的不同，vue的优缺点？
- vue v-modle实现原理
- http 缓存
- cookie可设置哪些属性？httponly?
- 登录后，前端做了哪些工作，如何得知已登录
- xss
- setTimeout时间延迟为何不准
- 事件循环述，宏任务和微任务有什么区别？
- let const var作用域
- 项目结构
- 数组排重，多种方法
- 实现sum(1,2,3,4..n)转化为 sum(1)(2)(3)(4)...(n)
- node 使用场景，express如何实现304

