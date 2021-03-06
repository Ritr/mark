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
    
  - this
  
    [tihs](https://segmentfault.com/a/1190000017452514)\
    this是Javascript语言的一个关键字。 它代表函数运行时，自动生成的一个内部对象，只能在函数内部使用。随着函数使用场合的不同，this的值会发生变化。但是有一个总的原则，那就是this指的是，调用函数的那个对象
    
  - 深拷贝浅拷贝
  
    深拷贝是递归复制了一个对象的属性和值到另一个对象上

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

- **css**

  - 标准盒模型
  
    ![image](https://images2015.cnblogs.com/blog/749461/201611/749461-20161108203732874-400170050.png)

  - IE盒模型

    ![image](https://images2015.cnblogs.com/blog/749461/201611/749461-20161108205109358-299654070.png)

  - 兼容写法
  
    头部加入
    ```
    <!doctype html public "-//w3c//dtd xhtml 1.0 transitional//en" "http://www.w3.org/tr/xhtml1/dtd/xhtml1-transitional.dtd">
    ```

- **html5**

  - Web Worker
    
    [Web Worker 使用教程](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)

    注意，这种多线程能力不是JavaScript语言原生具有的，而是浏览器宿主环境提供的。
    
    还有一个有意思的东西 shared worker，可以多页面共享一个woker以此来实现页面之间的通信

  - WebSocket
    
    >WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。
    WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。
    
    需要注意一点，服务端也要支持WebSocket。在node环境下可以试试 `socket.io`

- **css3**

  - flex布局
    
    掌握flex关键在于掌握两个轴：main axis和cross axis.

    main aixs即是主轴，cross axis即是和主轴交叉的轴，可以叫它交叉轴，实在不好翻译。
    
    注意当main aixs方向改变时（水平->垂直 或者 垂直->水平），cross axis也会随着改变

    [在线demo](https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/)

  - animation
    
    animation可以理解为像电影胶卷一样，让元素在某个时间段处于某种表现方式

    [https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)
    
  - transition
  
    trabsition相当于只有两个关键帧的animation，一个是开始状态一个是结束状态。

    [https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)
    
  - transform
    
    transform是干嘛的呢？它是控制元素的缩放，旋转，位移等属性的。transform使元素变成了舞蹈家。
    [https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)

  - @font-face
 
    为什么要把字体列出来呢？因为有了这个神器，网页中的图标都被解放了！将图标转换成矢量字体，或者直接用图标（字体）库，实现效果杠杠的！简直就是健康美味，好吃不贵！
    
    [https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face)

- **RESTful和状态码**
    
    RESTful是一种风格而不是规范，具体API设计还要结合本身的开发情况来考虑
    
    [RESTful API 最佳实践](http://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html)
    
- **优化**
  - 减少请求次数\
  合并图片、js、css
  - 减少请求体积\
  压缩图片、js、css
  - 懒加载\
  对非必须立刻展示的内容，延迟加载或者懒加载（需要时再加载）
  - 预加载\
  将资源提前加载到浏览器备用
  - 缓存\
  首页静态化，redis缓存，网站缓存，CDN缓存，客户端缓存。
- **工程化**  

   工程化是必须的

   [https://roshanca.com/2017/front-end-engineering-system/](https://roshanca.com/2017/front-end-engineering-system/)
### http和https

[链接一](http://www.mahaixiang.cn/internet/1233.html)

[链接二](https://juejin.im/post/5af557a3f265da0b9265a498#heading-42)

### DOM事件
[深入理解DOM事件机制](https://juejin.im/post/5c71e80d51882562547bb0ce#heading-22)

### js执行机制

[这一次，彻底弄懂 JavaScript 执行机制](https://juejin.im/post/59e85eebf265da430d571f89)

### Promise
[面试精选之Promise](https://juejin.im/post/5b31a4b7f265da595725f322)

### js数组方法总览

[js数组方法总览](https://juejin.im/post/5bb753bd6fb9a05d2272b673)

### cookie、session、localStorage、sessionStorage

[一文理解 cookie、localStorage、sessionStorage、session](https://juejin.im/post/5d82e46a51882556ba55e6a5#heading-18)

[localstorage 必知必会](https://juejin.im/post/5a9fcc5e51882555602074e3#heading-6)

**localstorage容量限制**

目前业界基本上统一为5M。

**cookie大小和数量**

cookie 的总数量没有限制，但是每个域名的COOKIE 数量和每个COOKIE 的大小是有限制的！

IE 每个域名限制为50 个。Firefox 每个域名cookie 限制为50 个。

Opera 每个域名cookie 限制为30 个。

Safari/webkit 貌似没有cookie 限制。

但是假如cookie 很多，则会使header大小超过服务器的处理的限制，会导致错误发生。

不同浏览器间每个cookie 文件大小也不同

Firefox 和safari 是4097 个字节，包括名（name）、值（value）和等号。

Opera 是4096 个字节，包括：名（name）、值（value）和等号。

IE 是4095 个字节，包括：名（name）、值（value）和等号。

记住最大4K

### css预处理语言

[sass](https://www.sass.hk/guide/)

[less](http://lesscss.cn/)

### css选择器

[css选择器](http://note.youdao.com/noteshare?id=46ea0a87d796bace083043735edd6b03&sub=2A8EB3A6438D4593ABEB907B49DD4C00)



### css权重
[你对CSS权重真的足够了解吗？](https://juejin.im/post/5afa98bf51882542c832e5ec)

### css盒模型

  - 标准盒模型
  
    ![image](https://images2015.cnblogs.com/blog/749461/201611/749461-20161108203732874-400170050.png)

  - IE盒模型

    ![image](https://images2015.cnblogs.com/blog/749461/201611/749461-20161108205109358-299654070.png)

  - 兼容写法
  
    头部加入，采用标准盒模型
    ```
    <!doctype html public "-//w3c//dtd xhtml 1.0 transitional//en" "http://www.w3.org/tr/xhtml1/dtd/xhtml1-transitional.dtd">
    ```
### flex布局
[一劳永逸的搞定 flex 布局](https://juejin.im/post/58e3a5a0a0bb9f0069fc16bb)

### webpack

[webpack官网](https://www.webpackjs.com/)

[B站珠峰架构-webpack](https://www.bilibili.com/video/av51693431?from=search&seid=13071479149774343245)

### js优化问题

### js变量、函数、数据类型转换和比较、作用域、作用域链、闭包

在javascript权威指南里

