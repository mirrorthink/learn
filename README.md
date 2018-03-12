# learn
>下面的文章都是我在学习过程各处收集来的，目的是为了更好的查阅

- [Markdown——入门指南](https://www.jianshu.com/p/q81RER)
- [阮一峰es6电子书](http://es6.ruanyifeng.com)
- [笔试面经网](https://www.nowcoder.com)
- [正则](https://baike.baidu.com/item/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F/1700215?fr=aladdin)
- [手动实现mvvm](https://www.imooc.com/article/22065?block_id=tuijian_wz)
- [vue源码学习](https://www.imooc.com/article/22102)
- [vueDD源码学习](https://github.com/DDFE/DDFE-blog)


#### [URL 输入到页面展现的过程简述](https://www.jianshu.com/p/63166522c244)
>浏览器在解析过程中，如果遇到请求外部资源时请求过程是异步的，并不会影响HTML文档进行加载，但是当文档加载过程中遇到JS文件，HTML文档会挂起渲染过程，不仅要等到文档中JS文件加载完毕还要等待解析执行完毕，才会继续HTML的渲染过程。原因是因为JS有可能修改DOM结构，这就意味着JS执行完成前，后续所有资源的下载是没有必要的，这就是JS阻塞后续资源下载的根本原因。CSS文件的加载不影响JS文件的加载，但是却影响JS文件的执行。JS代码执行前浏览器必须保证CSS文件已经下载并加载完毕

>当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，而@import引用的CSS会等到页面全部被下载完再被加载。
#### sessionStorage 、localStorage 和 cookie 之间的区别
>共同点：都是保存在浏览器端，且同源的。
区别：cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递；cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下。存储大小限制也不同，cookie数据不能超过4k，同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如会话标识。
而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。
> - 数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此 用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。
> - 作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。Web Storage 支持事件通知机制，可以将数据更新的通知发送给监听者。Web Storage 的 api 接口使用更方便。
如果您在cookie中设置了HttpOnly属性，那么通过js脚本将无法读取到cookie信息，这样能有效的防止XSS攻击


[http缓存相关](https://www.cnblogs.com/chenqf/p/6386163.html)
##### 强制缓存
>如果生效，不需要再和服务器发生交互，而对比缓存不管是否生效，都需要与服务端发生交互。两类缓存规则可以同时存在，强制缓存优先级高于对比缓存
对于强制缓存来说，响应header中会有两个字段来标明失效规则（Expires/Cache-Control）
> - Expires到期时间是由服务端生成的，但是客户端时间可能跟服务端时间有误差，这就会导致缓存命中的误差。
> - Cache-Control 是最重要的规则。常见的取值有private、public、no-cache、max-age，no-store，默认为private。
>   1. private:             客户端可以缓存
>   2. public:              客户端和代理服务器都可缓存（前端的同学，可以认为public和private是一样的）
>   3. max-age=xxx:   缓存的内容将在 xxx 秒后失效
>   4. no-cache:          需要使用对比缓存来验证缓存数据（后面介绍）
>   5. no-store:           所有内容都不会缓存，强制缓存，对比缓存都不会触发
##### 对比缓存
>顾名思义，需要进行比较判断是否可以使用缓存。
浏览器第一次请求数据时，服务器会将缓存标识与数据一起返回给客户端，客户端将二者备份至缓存数据库中。
再次请求数据时，客户端将备份的缓存标识发送给服务器，服务器根据缓存标识进行判断，判断成功后，返回304状态码，通知客户端比较成功，可以使用缓存数据。
> - Last-Modified（响应头）：服务器在响应请求时，告诉浏览器资源的最后修改时间。
> - If-Modified-Since(请求头)：再次请求服务器时，通过此字段通知服务器上次请求时，服务器返回的资源最后修改时间。
> -Etag（响应头）：服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识（生成规则由服务器决定）。

>对于强制缓存，服务器通知浏览器一个缓存时间，在缓存时间内，下次请求，直接用缓存，不在时间内，执行比较缓存策略。
对于比较缓存，将缓存信息中的Etag和Last-Modified通过请求发送给服务器，由服务器校验，返回304状态码时，浏览器直接使用缓存。
#### webpack 原理
> 一切皆为模块，由于webpack并不支持除.js以外的文件，从而需要使用loader转换成webpack支持的模块，plugin用于扩展webpack的功能，在webpack构建生命周期的过程在合适的时机做了合适的事情。[webpack教程推荐](http://array_huang.coding.me/webpack-book/chapter0/preface.html)
##### Webpack从构建到输出文件结果的过程：
> 1. 解析配置参数，合并从shell传入和webpack.config.js文件的配置信息，输出最终的配置信息
> 2. 注册配置中的插件，好让插件监听webpack构建生命周期中的事件节点，做出对应的反应
> 3. 解析配置文件中entry入口文件，并找出每个文件依赖的文件，递归下去
> 4. 在递归每个文件的过程中，根据文件类型和配置文件中loader找出相对应的loader对文件进行转换
> 5. 递归结束之后得到每个文件最终的结果，根据entry配置生成代码chunk
> 6. 输出所有chunk到文件系统
#### css 左侧固定 右侧自适应
>这种方法我采用的是左边浮动，右边加上一个margin-left值，让他实现左边固定，右边自适应的布局效果
position：
#### Karma是一个基于Node.js的JavaScript测试执行过程管理工具（Test Runner）
##### Jasmine是单元测试框架
#### 原型链
##### __proto__ 与prototype的区别
`
var f = new F(); 
//于是有
f.__proto__ === F.prototype //true
//对象具有属性__proto__，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型，这也保证了实例能够访问在构造函数原型中定义的属性和方法
//又因为
F.prototype === o;//true
//所以
f.__proto__ === o;
`
> 1.在JS里，万物皆对象。方法（Function）是对象，方法的原型(Function.prototype)是对象。因此，它们都会具有对象共有的特点。即：对象具有属性__proto__，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型，这也保证了实例能够访问在构造函数原型中定义的属性和方法。2.方法(Function)方法这个特殊的对象，除了和其他对象一样有上述_proto_属性之外，还有自己特有的属性——原型属性（prototype），这个属性是一个指针，指向一个对象，这个对象的用途就是包含所有实例共享的属性和方法（我们把这个对象叫做原型对象）。原型对象也有一个属性，叫做constructor，这个属性包含了一个指针，指回原构造函数。
1.对象有属性__proto__,指向该对象的构造函数的原型对象。
2.方法除了有属性__proto__,还有属性prototype，prototype指向该方法的原型对象。

#### ES6 模块与 CommonJS 模块的差异
> CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

#### node的事件循环模型
>  1.在进程启动时，Node便会创建一个类似while(true)的循环，没执行一次循环体的过程我们称为tick,每个tick的过程就是查看是否有事件待处理，有则取出并执行。一直循环直到无事件，退出循环。
2.异步IO网络事件等是事件的产生者，这些事件被传递到对应的观察者那里，事件循环从观察者那里取出事件并处理

![Alt text](http://www.runoob.com/wp-content/uploads/2015/09/event_loop.jpg)

#### promise原理
>  在then方法中储存回调函数，调用resolve执行回调


#### node 中间件
ͭ> 通过app.use 将  中间件加入队列 app.stack=[] 数组队列 中间件实现一个next方法 ，取出中间件并执行，同时传入当前方法以实现递归调用，达到持续触发的目的。

#### css 一侧定宽，一侧自适应，且高度自适应 均为100% 
> 父元素 绝对定位 且固定宽高，若高度相对屏幕，则可不设置宽高，直接设置top、bottom、left、right的值。左元素设定宽，左浮动，高100%，右边元素设置margin-left，高100%

#### bind 与call、apply的区别
> bind是引用（不会马上执行），call、apply就是直接执行调用函数
#### ajax原理
>  xmlhttp = new XmlHttpRequest();

#### w3c事件机制
> 任何事件首先向下传播直到遇到目标元素，然后再向上冒泡返回
阻止事件冒泡，阻止默认事件，event.stopPropagation()和event.preventDefault()，return false
 
