- **js**
  - 闭包\
  要理解闭包，首先要知道javascript的作用域。通常javascript作用域分为全局作用域和函数内作用域，通常来说一个函数执行开始到结束也意味着一个作用域的创建到销毁，如果函数A内变量被引用，则A会在内存中驻留一段时间直至A内变量都被释放，我们就可以将这个函数作用域称之为闭包。也可以这么说，闭包是函数作用域的一种使用方式的实现。使用闭包会引起内存升高，应尽量规避闭包，使用let替代var是一种非常好的方式。因为let的作用域是大括号内。
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
    > Promise
    
    > async await
    
  - this\
  this即是句柄，谁执行谁就是this
  - 深拷贝浅拷贝
  - 箭头函数和箭头函数的this
  - es6、7新增语法、方法、特性
  - 防抖节流
- **DOM**
  - 事件冒泡
  - 事件委托
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



4. promise与fetch区别
5. react组件的生命周期
6. UI组件与容器组件
7. redux/vuex
8. 前端性能优化
9. 浏览器存储原理
10. webpack配置
11. react路由/vue-router
12. promise跨域
13. vue双向绑定原理
14. vue和react的区别

