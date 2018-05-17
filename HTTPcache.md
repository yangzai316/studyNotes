# HTTP 缓存
## 官方解释
先来一段百度百科的解释：
> 浏览器缓存（Browser Caching）是为了节约网络的资源加速浏览，浏览器在用户磁盘上对最近请求过的文档进行存储，当访问者再次请求这个页面时，浏览器就可以从本地磁盘显示文档，这样就可以加速页面的阅览。
## 通俗解释：
有部分文件，比如某个js文件，长时间没有被修改和操作，好比引用的Jquery.js，可能几年都不会修改一下，这种文件，肯定不能每次客户端刷新页面的时候都从服务器下载一次，
这就是多余的请求，那么浏览器可以缓存一个信息，这个信息告诉服务器，这个文件不需要从新返回，可以使用缓存中的文件，这就涉及到HTTP缓存，也就是浏览器缓存。
## 为什么需要HTTP缓存
浏览器缓存可以在一定程度上避免不必要的数据请求，减少服务器开销，避免带宽浪费。
## 如何实现缓存的？
缓存一般就两种：**强缓存、协商缓存**。</br>
一句话：再次请求的header头部，携带信息，先验证是否命中强缓存，命中就是用缓存文件，没有命中，就验证是否命中协商缓存，命中就用缓存，还是没有命中就再次请求服务器。
这个过程如下图：</br>
 ![http缓存](https://raw.githubusercontent.com/yangzaiwangzi/studyNotes/master/img/httpcache/http%E7%BC%93%E5%AD%98.jpg)</br>
下面详细解释一下，强缓存和协商缓存；
## 强缓存
响应头中直接通过下面的字段定义是否需要缓存，如何缓存。</br>
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
 ![强缓存](https://raw.githubusercontent.com/yangzaiwangzi/studyNotes/master/img/httpcache/%E5%BC%BA%E7%BC%93%E5%AD%98.jpg)</br>
## 协商缓存
当没有命中强缓存，则会验证协商缓存。</br>
协商缓存有两种形式：*文件最后一次修改时间*、*与文件内容对应的hash值*
### 通过文件最后一次修改时间
上次一个请求返回的Reponse中会有Last-modified，携带着和服务器中存储着一样的最后一次文件修改的时间，再次请求时request会携带If-Modified-Since（就是Last-modified）和服务器存储的最后一次文件修改的时间比对，如果一样就是没有修改文件，则命中，反之亦然。
### 通过与文件内容对应的hash值
最后一次文件修改时间不一样，不代表文件确实被修改过了，比如：修改了某文件，有修改回来了，这样文件的修改时间发生变化，但是文件的内容没有变化，所以不同的会生成唯一的hash与之对应，在上次一个请求返回的Reponse中的ETag返回给客户端，再次请求时request会携带If-Modified-Match（就是ETag）与服务器存储的hash对比，一样则没有修改文件，则命中，</br>
过程如下图：</br>
 ![强缓存](https://raw.githubusercontent.com/yangzaiwangzi/studyNotes/master/img/httpcache/%E5%8D%8F%E5%95%86%E7%BC%93%E5%AD%98.jpg)</br>
## 最后
至此，HTTP缓存，就差不多结束了，整体的过程如下图：</br>
 ![强缓存](https://raw.githubusercontent.com/yangzaiwangzi/studyNotes/master/img/httpcache/http%E7%BC%93%E5%AD%98%E8%AF%A6%E7%BB%86.jpg)</br></br>
 *有帮助STAR我，有问题Issues我，谢谢*
