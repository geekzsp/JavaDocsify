

# Java Web TODO

* Servlet 

接收用户请求 HttpServletRequest 在doGet() 或者doPost中做相应处理 返回HttpServletResponse
init service destroy
一个Servlet 只会有一个实例 所以不是线程安全的

* 转发(Forward) 和重定向(Redirect) 区别
  * 转发:服务器行为  重定向:客户端行为 302 +location
  * 转发 只能跳转 本web应用内页面
  * 地址栏 ：  转发 显示原来的地址
  * 数据共享： 转发页面和转发到的页面可以共享request里面的数据
  * 运用地方：forward:一般用于用户登陆的时候,根据角色转发到相应的模块. redirect:一般用于用户注销登陆时返回主页面和跳转到其它的网站等
    效率： 转发高
* JSP 侧重视图 Servlet侧重逻辑控制

JSP 是在第一次请求的是时候被编译 work/Catalina/
JSP 9大内置对象
request response pageContext session application out config page exception

* Cookie 在客户端 Session在服务器端  因为Http协议是无状态的 会话跟踪 维持会话  现在Token用的比较多

# OAuth2协议

## 应用场景

如：有一个"云冲印"的网站，可以将用户储存在Google的照片，冲印出来。用户为了使用该服务，必须让"云冲印"读取自己储存在Google上的照片。

直接给他们账号密码是不安全的，需要一种安全的授权机制。

## 几种授权模式

* 客户端的授权模式

* 授权码模式

  >（A）用户访问客户端，后者将前者导向认证服务器。  
  >（B）用户选择是否给予客户端授权。       
  >（C）假设用户给予授权，认证服务器将用户导向客户端事先指定的"重定向URI"（redirection URI），同时附上一个授权码。     
  >（D）客户端收到授权码，附上早先的"重定向URI"，向认证服务器申请令牌。这一步是在客户端的后台的服务器上完成的，对用户不可见。   
  >（E）认证服务器核对了授权码和重定向URI，确认无误后，向客户端发送访问令牌（access token）和更新令牌（refresh token）。 

* 简化模式

简化模式（implicit grant type）不通过第三方应用程序的服务器，直接在浏览器中向认证服务器申请令牌，跳过了"授权码"这个步骤，因此得名。所有步骤在浏览器中完成，令牌对访问者是可见的，且客户端不需要认证。

* 密码模式
* 客户端模式

