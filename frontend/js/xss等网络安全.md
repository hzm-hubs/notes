### XSS-跨域脚本：向网页植入恶意脚本


* 反射型（非持久）
一般需要用户主动点击，执行URL传递参数的功能（网络搜索、跳转），该链接包含恶意脚本，当用户点击时，恶意脚本被发送到服务器，然后立即反射回用户的浏览器执行。

* 存储型（持久性）
存储在服务器端，所有访问的用户都会在其浏览器中执行

* DOM-based XSS
当页面的Document Object Model（DOM）被恶意脚本修改，并且这些修改导致浏览器执行了恶意操作时发生的XSS攻击。

处理：
* 限制只能同域名下的资源链接才可以加载，减少XSS攻击的机会。
* 输入过滤：对所有用户输入进行过滤，不允许 <code>script</code> <code>iframe</code> 等潜在危险的HTML标签被输入。
* 对敏感字符进行转义后再插入到页面中，如手机号
* 验证码：防止脚本冒充用户提交危险操作。
* 使用HTTP-only Cookies：设置HTTP-only标志，使得Cookie不能通过客户端脚本访问。


### CSRF：从其他网站向本网站发起攻击

处理：
* 1.同源检测
* 2.在提交表单时进行CSRF的token校验+cookie验证


### SQL注入
将恶意SQL插入参数重，在后台SQL服务器上解析执行