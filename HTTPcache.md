# HTTP 缓存
## 官方解释
先来一段百度百科的解释：
> 浏览器缓存（Browser Caching）是为了节约网络的资源加速浏览，浏览器在用户磁盘上对最近请求过的文档进行存储，当访问者再次请求这个页面时，浏览器就可以从本地磁盘显示文档，这样就可以加速页面的阅览。
## 通俗解释：
有部分文件，比如某个js文件，长时间没有被修改和操作，好比引用的Jquery.js，可能几年都不会修改一下，这种文件，肯定不能每次客户端刷新页面的时候都从服务器下载一次，
这就是多余的请求，那么浏览器可以缓存一个信息，这个信息告诉服务器，这个文件不需要从新返回，可以使用缓存中的文件，这个过程就是HTTP缓存，也就是浏览器缓存。
## 如何实现缓存的？
缓存一般就两种：**强缓存、协商缓存**。</br>
一句话：再次请求的header头部，携带信息，先验证是否命中强缓存，命中就是用缓存文件，没有命中，就验证是否命中协商缓存，命中就用缓存，还是没有命中就再次请求服务器。
这个过程如下图：</br>
 ![http缓存](https://raw.githubusercontent.com/yangzaiwangzi/studyNotes/master/img/httpcache/http%E7%BC%93%E5%AD%98.jpg)</br>
下面详细解释一下，强缓存和协商缓存；
## 强缓存
主要是通过判断文件最后一次修改的时间是否匹配，来判断是否需要使用缓存。</br>
相关请求头字段：</br>
### Cache-Control
Cache-Control 是 Http/1.1 新增的字段，是控制浏览器缓存的主要字段。</br> 
no-cache：资源可以被缓存，但立刻过期，下次访问必须验证资源有效性</br>
max-age：缓存的内容将在 xxx 秒后失效, 这个选项只在HTTP 1.1可用, 并如果和Last-Modified一起使用时, 优先级较高</br>
no-store：必须先与服务器确认返回的响应是否被更改，然后才能使用该响应来满足后续对同一个网址的请求。因此，如果存在合适的验证令牌 (ETag)，no-cache 会发起往返通信来验证缓存的响应，如果资源未被更改，可以避免下载。</br>
public：资源可以被浏览器和代理服务器缓存</br>
private： 资源只能被浏览器缓存</br>
### Pragma
Pragma 是 Http/1.0 的头部字段，只有一个值 no-cache， 功能和 Cache-Control:no-cache 一样。
### Expires
Expires 是缓存到期时间，以服务器时间为参考，优先级比 Cache-Control: max-age 低。
过程如下图</br>
 ![强缓存](https://raw.githubusercontent.com/yangzaiwangzi/studyNotes/master/img/httpcache/http%E7%BC%93%E5%AD%98.jpg)</br>
