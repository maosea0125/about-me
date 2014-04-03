Github不能加载JS/CSS的问题
--------------------------

是因为github的CDN为fastly.net的，但是不巧的是，上面url中的ssl是GFW的敏感字，直接中招.

#### 解决办法

修改HOST文件，通过www.ipaddress.com查询github.global.ssl.fastly.net的IP地址，然后加入HOST文件：
<pre>
#fix github can not load js/css
185.31.17.184  github.global.ssl.fastly.net
</pre>