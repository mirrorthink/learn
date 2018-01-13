# learn
[Markdown——入门指南](https://www.jianshu.com/p/1e402922ee32/)
[阮一峰es6电子书](http://es6.ruanyifeng.com)
笔试面经网](https://www.nowcoder.com)
[正则](https://baike.baidu.com/item/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F/1700215?fr=aladdin)

[URL 输入到页面展现的过程简述](https://www.jianshu.com/p/63166522c244)
>浏览器在解析过程中，如果遇到请求外部资源时请求过程是异步的，并不会影响HTML文档进行加载，但是当文档加载过程中遇到JS文件，HTML文档会挂起渲染过程，不仅要等到文档中JS文件加载完毕还要等待解析执行完毕，才会继续HTML的渲染过程。原因是因为JS有可能修改DOM结构，这就意味着JS执行完成前，后续所有资源的下载是没有必要的，这就是JS阻塞后续资源下载的根本原因。CSS文件的加载不影响JS文件的加载，但是却影响JS文件的执行。JS代码执行前浏览器必须保证CSS文件已经下载并加载完毕


>当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，而@import引用的CSS会等到页面全部被下载完再被加载。

>sessionStorage 、localStorage 和 cookie 之间的区别
共同点：都是保存在浏览器端，且同源的。
区别：cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递；cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下。存储大小限制也不同，cookie数据不能超过4k，同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如会话标识。
而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。
数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。
作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。Web Storage 支持事件通知机制，可以将数据更新的通知发送给监听者。Web Storage 的 api 接口使用更方便。
如果您在cookie中设置了HttpOnly属性，那么通过js脚本将无法读取到cookie信息，这样能有效的防止XSS攻击
>sss
>ss ###辅导费胜多负少
>
[http缓存相关](https://www.cnblogs.com/chenqf/p/6386163.html)
>###强制缓存
如果生效，不需要再和服务器发生交互，而对比缓存不管是否生效，都需要与服务端发生交互。两类缓存规则可以同时存在，强制缓存优先级高于对比缓存
对于强制缓存来说，响应header中会有两个字段来标明失效规则（Expires/Cache-Control）
Expires到期时间是由服务端生成的，但是客户端时间可能跟服务端时间有误差，这就会导致缓存命中的误差。
Cache-Control 是最重要的规则。常见的取值有private、public、no-cache、max-age，no-store，默认为private。
private:             客户端可以缓存
public:              客户端和代理服务器都可缓存（前端的同学，可以认为public和private是一样的）
max-age=xxx:   缓存的内容将在 xxx 秒后失效
no-cache:          需要使用对比缓存来验证缓存数据（后面介绍）
no-store:           所有内容都不会缓存，强制缓存，对比缓存都不会触发
###对比缓存
，顾名思义，需要进行比较判断是否可以使用缓存。
浏览器第一次请求数据时，服务器会将缓存标识与数据一起返回给客户端，客户端将二者备份至缓存数据库中。
再次请求数据时，客户端将备份的缓存标识发送给服务器，服务器根据缓存标识进行判断，判断成功后，返回304状态码，通知客户端比较成功，可以使用缓存数据。
Last-Modified（响应头）：服务器在响应请求时，告诉浏览器资源的最后修改时间。
If-Modified-Since(请求头)：再次请求服务器时，通过此字段通知服务器上次请求时，服务器返回的资源最后修改时间。
Etag（响应头）：服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识（生成规则由服务器决定）。
对于强制缓存，服务器通知浏览器一个缓存时间，在缓存时间内，下次请求，直接用缓存，不在时间内，执行比较缓存策略。
对于比较缓存，将缓存信息中的Etag和Last-Modified通过请求发送给服务器，由服务器校验，返回304状态码时，浏览器直接使用缓存。
