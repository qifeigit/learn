## 认证原理

1.用户访问业务系统。(比如：[http://localhost:8080](http://localhost:8080/))

2.如果已经在业务系统登录 (Y) 就直接进行后续操作。

3.如果尚未在业务系统登录 (N) 就跳入第4步。

4.业务系统使用自己的url和cas服务器的url，生成一个https://casdev.office.cn/login?service=http://localhost:8080，然后告知用户浏览器使用302跳转到这个url。

5.cas接收到上面的url，先判断用户是否已经在cas登录。

6.如果已经在cas登录 (Y) 就进入第11步。

7.如果尚未在cas登录 (M) 就进入第8步。

8.显示登录页面，等待用户输入账号和密码进行登录。

9.如果登录成功 (Y) 就进入第11步。

10.如果登录失败 (Y) 就显示错误提示，继续跳转到第8步，显示登录页面等待用户登录。

11.cas生成一个serviceTicket，这个serviceTicket与当前登录用户关联，并且是唯一的，cas使用第4步传递来的service参数和serviceTicket生成一个url：类似http://localhost:8080?ticket=servietTicket，然后告知用户浏览器使用302跳转到这个url。

12.业务系统接收到http://localhost:8080?ticket=servietTicket，获得url上的ticket参数，然后直接通过http请求，将ticket参数传递给cas服务器，cas服务器会返回ticket对应的账号。业务系统会信任cas服务器返回的账号，并将这个账号设置为已登陆的用户。（一般是保存在session里）