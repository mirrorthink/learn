# learn
[Markdown——入门指南](https://www.jianshu.com/p/1e402922ee32/)

[URL 输入到页面展现的过程简述](https://www.jianshu.com/p/63166522c244)
>浏览器在解析过程中，如果遇到请求外部资源时请求过程是异步的，并不会影响HTML文档进行加载，但是当文档加载过程中遇到JS文件，HTML文档会挂起渲染过程，不仅要等到文档中JS文件加载完毕还要等待解析执行完毕，才会继续HTML的渲染过程。原因是因为JS有可能修改DOM结构，这就意味着JS执行完成前，后续所有资源的下载是没有必要的，这就是JS阻塞后续资源下载的根本原因。CSS文件的加载不影响JS文件的加载，但是却影响JS文件的执行。JS代码执行前浏览器必须保证CSS文件已经下载并加载完毕


