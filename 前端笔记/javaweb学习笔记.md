# javaweb学习笔记

> 主要参考资料：
>
> 1. 【尚硅谷】java web零基础入门完整版(bilibili)

目录

### 基本概念

javaweb：通过 Java 语言编写可以通过浏览器访问的程序。是基于请求和响应来开发的。

### 网页结构

数据内容（HTML）+静态表现（CSS）+交互行为（JavaScript）

### HTML基础

Hyper Text Markup Language （超文本标记语言）

使用标签来标记要显示的网页中的各个部分。通过在文本文件中添加 标记符？，可以告诉浏览器如何显示其中的内容。

.html文件直接由浏览器解析执行。

代码模板：

```html
<html>
	<head>
		头信息（可用于引入css、js等）
		<title>标题</title>
	</head>
	<body>
		主体内容
	</body>
</html>
```

#### 基本语法

`<【双标签】>【数据内容】</【双标签】>` 或 `<【单标签】 【数据内容】/>`

标签大小写不敏感

##### 注释

```html
<!--【注释】-->
```

##### 属性

分为基本属性、事件属性

写在标签名后

常用的：

* 字体 `<font color="" face="字体" size="">`
* 粗体b、段落p、换行br、标题h1~h6、独占一行div
* 超链接 `<a href="url" target="打开方式：默认_self当前页面 或 _blank新页面">`
* base地址（指定一个相对路径计算时固定的绝对路径）`<base href="url">`
* 图片 `<img src="url" width="" height="" >`
* 表格 `<table border="" align=""  width="" height="">` （嵌套 行tr 嵌套 表头th/单元格td colspan="跨行数" rowspan="跨列数"）
* 无序列表ul（嵌套 列li）、有序列表ol（嵌套 列li）
* 表单（表示允许用户输入）（只有自定义了name属性值的表单项才会作为请求参数提交给服务器）
  ```html
  <form action="提交到的服务器" method="提交方式"> 
  	<input type="文本域text/文件上传域file/按钮button/单选按钮radio/复选框checkbox/提交表单按钮submit/重置表单按钮reset" name="表单项名" value="表单项默认值">
  	<textarea rows="" cols="">默认值</textarea>多行文本输入框
  	<select>下拉列表框
  		<option>选项<option>
  	<select>
  </form>
  ```
* 内嵌窗口iframe

##### 字符实体

部分字符在html被解析时有特殊含义，如需用于数据内容须改写为对应的字符实体名

| 显示结果 | 描述   | 实体名称 |
| -------- | ------ | -------- |
|          | 空格   | &nbsp    |
| <        | 小于号 | &lt      |
| >        | 大于号 | &gt      |
| &        | 和号   | &amp     |
| "        | 引号   | &quot    |
| '        | 撇号   | &apos    |

### CSS基础

Cascading Style Sheet 层叠样式表单

用于(增强)控制网页样式并允许将样式信息与网页内容分离的一种标记性语言。

#### 基本语法

【选择器】{【属性名】:【属性值】;...}

##### 选择器

表示作用的元素。

常用的类型有：

* 标签选择器：对应html中的标签名
* id选择器： `#【id】`：在html的标签中应用只需添加属性 `id=...`，一个元素（标签）只能用一个id
* 类选择器：`【标签名】.【class值】`：在html的对应标签中应用只需添加属性 `class=...`，标签名可省略，一个元素（标签）能用多个class（用空格分隔即可）
* 属性选择器
* 组合选择器：`【选择器1】,【选择器2】,...`

##### 属性

color、background-color、width、height、border、border-collapse、font-size、margin-left、margin-right、text-align

##### 注释

`/*...*/`

### HTML + CSS

#### 内联样式法

将css的属性设置内嵌到html的标签中： `style="【属性名】:【属性值】;..."`

#### 内部样式块法

在html的head中定义标签 `<style type="text/css">`来封装css代码

#### 链接外部样式表文件法

在html的head中定义标签 `<link rel="stylesheet" type="text/css" href="xxx.css" />` 导入 css 样
式文件

### JavaScript基础

参见 JavaScript学习笔记.md

### HTML+JS

#### 内联法

在html的head中定义标签 `<script type="text/javascript">`来封装JavaScript代码

#### 链接外部JS文件法

在html的head中定义标签 `<script type="text/javascript" src="xxx.js"></script>`导入 js文件

### XML基础

一种可扩展的标记性语言。

常作为存储配置文件

#### .xml声明

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

#### 基本语法

（类似html）

<【元素名】>【封装内容】<【元素名】/>

* 元素名不能以数字或者标点符号开始，不能含空格
* 大小写敏感
* 整个xml文档需有根元素
* 文本区域：

```xml
<![CDATA[ 这里可以把你输入的字符原样显示，被解析]]>
```

#### dom4j

是一种封装了DOM的第三方的标记语言解析技术

常用于将xml文档中的标签解析为java实体类对象

使用时可以类库的形式(.jar)引入

常用模板：

```java
public void readXML() throws DocumentException {
	SAXReader reader = new SAXReader();
	Document document = reader.read("xxx.xml");
	Element rootElement = document.getRootElement();
	List<Element> elements= rootElement .elements("【标签名】");
	for (Element e: elements) {
		String 【子标签的文本内容】=e.elementText("【子标签】");
		...
		【实体类】【实体类对象】=new 【实体类】(...);
		...
	}
}
```

### Tomcat

由 Apache 组织提供的一种轻量级的JavaWeb服务器。

支持 jsp 和 Servlet 。

#### 项目部署

### Servlet

是JavaEE的一种程序规范（模板），本质上是个接口

用于运行在服务器上，接收客户端发送过来的请求，并响应数据给客户端。

Servlet程序是一种浏览器可访问的多态资源。

#### 基础配置

在Servlet程序所在的项目的web.xml中配置：

```xml
<servlet>
	<servlet-name>【程序别名】</servlet-name>
	<servlet-class>【程序类名】</servlet-class>
	<init-param>//初始化参数，相当于类的静态变量
		<param-name>【初始化参数名】</param-name>
		<param-value>【初始化参数值】</param-value>
	</init-param>
</servlet>

<servlet-mapping>
	<servlet-name>【程序别名】</servlet-name>
	<url-pattern>/【访问地址】</url-pattern>
</servlet-mapping>

<context-param>//上下文参数，作用域在整个工程
	<param-name>【上下文参数名】</param-name>
	<param-value>【上下文参数值】</param-value>
</context-param>
```

#### 生命周期

1. 执行 Servlet 构造器方法（第一次访问Servlet 程序/实现类会调用）
2. 执行 init 初始化方法（第一次访问Servlet 程序/实现类会调用）
3. 执行 service 方法（每次访问都会调用）
4. 执行 destroy 销毁方法（web 工程停止的时候调用）

可用路径参数action显式指定访问要调用的方法

#### 常用重写方法

##### init

`public void init(ServletConfig servletConfig)`

重写时需先调用父类同名方法

##### service

`public void service(ServletRequest servletRequest, ServletResponse servletResponse) `

获取http请求的请求方法类型：调用传入参数所实现的ServletRequest接口的子接口中的getMethod方法，即 `String method = ((HttpServletRequest)servletRequest).getMethod();`

#### HttpServlet类

Servlet接口的实现GenericServlet的子类，已实现service方法

##### 常用重写方法

###### doGet

`protected void doGet(HttpServletRequest req, HttpServletResponse resp)`

###### doPost

`protected void doPost(HttpServletRequest req, HttpServletResponse resp)`

#### ServletConfig类

第一次访问Servlet 程序/实现类时会创建其对应的ServletConfig对象，并作为init方法的传入参数

##### 常用方法

* getServletName()
* getInitParameter(【初始化参数名】)

#### ServletContext接口

存储Servlet 上下文信息。

一个 web 工程只有一个 ServletContext对象。在 web 工程部署启动的时候创建。在 web工程停止的时候销毁。

获取ServletContext对象：调用GenericServlet或ServletConfig的类方法getServletContext()

##### 常用方法

* getInitParameter(【上下文参数名】)
* getContextPath()工程路径
* getRealPath("/...")将相对路径转换为绝对路径
* setAttribute(key,value) getAttribute(key) 存储键值对（作为域对象使用）

#### HttpServletRequest 类

封装了每次的请求信息，作为doGet和doPost的传入参数

##### 常用方法

* getRequestURI() getRequestURL()
* getRemoteHost()获取客户端的ip地址
* getHeader()
* getParameter(【表单项的name】)getParameterValues(【表单项的name】)获取请求的参数
* getMethod()
* setAttribute(key,value) getAttribute(key)
* getRequestDispatcher()获取请求转发对象

#### HttpServletResponse类

封装了每次的响应信息，作为doGet和doPost的传入参数

##### 常用方法

* getOutputStream() getWriter() 获取输出流
* setContentType("text/html;charset=UTF-8")
* sendRedirect("【新地址】")请求重定向

#### 请求转发

一次请求需要连锁调用多个servlet程序，servlet程序之间的控制流称为请求转发

`httpServletRequest.getRequestDispatcher("【另一程序地址】").forward(httpServletRequest,httpServletResponse)`

### jsp

java server pages

文本格式和访问方式类似html，用于代替 Servlet 程序回传 html 页面数据。

本质上仍然是个Servlet 程序，第一次访问 jsp 页面时，Tomcat 服务器将其转换为java 源文件。

其中每个html标签数据都被转换到_jspService() 方法内的out.write()中

pageContext对象表示该jsp页面的上下文

#### 常用标签

##### page

`<%@ page 【属性】="【属性值】"%>`

用于设置jsp页面信息，常写在首行

常用属性：

* language="java"
* contentType返回的数据类型
* pageEncoding字符集
* import导包
* autoFlush System.out缓冲区满了自动刷新
* buffer System.out缓冲区大小
* errorPage运行出错时的跳转路径
* isErrorPage
* session是否创建session对象
* extends该java类继承的父类

##### include

在一个jsp页面内引入其他jsp页面

###### 静态包含

`<%@include file="/xxx.jsp"%>`

底层实现：直接复制jsp源码插入原位置

###### 动态包含

```html
<jsp:include page="/xxx.jsp">
	<jsp:param name="" value=""/>
</jsp:include>
```

底层实现：调用 `JspRuntimeLibrary.include(request,response,"/xxx.jsp",out,false);`，其中request、response、out以及其他自定义参数是共享的

##### forward

请求转发

`<jsp:forward page="/xxx.jsp"></jsp:forward>`

#### java脚本

将java代码内嵌雨jsp文件中

##### 声明脚本

`<%!【定义类的属性、方法、静态代码块、内部类等】%>`

##### 表达式脚本

`<%=【表达式】%>`

会被转换到_jspService() 方法内的out.print()中

##### 代码脚本

`<%【代码】%>`

会被转换到_jspService() 方法内

#### 其他

* out缓冲区数据会传递给respon.writer缓冲区，jsp中常用out代替writer
* out.write()字节输出（只能接受字符串），out.print()字符输出（可将任意数据转换为字符串再调用write）

#### EL表达式

Expression Language

用于代替jsp 页面中的表达式脚本

格式：`${【表达式】}`

* 可直接通过key调用域对象存储的value，会依次从小到大查找四个域对象的数据（pageContext request session application）
* empty运算符判断后缀表达式是否为空
* 可直接调用隐含变量获取请求信息（param paramValues header headerValues cookie initParam...）

#### JSTL 标签库

JSP Standard Tag Library

用于替换代码脚本

由五个子库组成：图

##### 导入

`<%@ taglib prefix="" uri="http://java.sun.com/jsp/jstl/..." %>`

##### core 核心库的常用标签

* set 往域对象中保存数据<c:set scope="【域对象】" var="key" value="value"/>
* if `<c:if test="${【表达式】}">...</c:if>`
* choose+when+otherwise 作用类似于switch
* forEach `<c:forEach begin="" end="" step="" items="${}" var="" >`

### Listener 监听器

是JavaEE的一种程序规范（模板），本质上是个接口

用于监听某种事物的变化，然后调用回调函数，反馈给客户（程序）去做一些相应的处理。

#### ServletContextListener接口

用于监听ServletContext 对象的创建和销毁

##### 重写方法

* public void contextInitialized(ServletContextEvent sce);
* public void contextDestroyed(ServletContextEvent sce);

##### 配置

在web.xml中

```xml
<listener>
	<listener-class>【监听器实现类名】</listener-class>
</listener>
```

### Filter 过滤器

是JavaEE的一种程序规范（模板），本质上是个接口

用于拦截请求（权限检查、日记操作、事务管理等），过滤响应

#### 重写方法

`public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain)`

方法中应调用 ` filterChain.doFilter(servletRequest,servletResponse);`使得程序向下继续执行其他过滤器或访问相关资源（顺序同配置顺序）

#### 配置

在web.xml中

```xml
<filter>
	<filter-name>【Filter别名】</filter-name>
	<filter-class>【Filter类名】</filter-class>
	<init-param>//初始化参数，相当于类的静态变量
		<param-name>【初始化参数名】</param-name>
		<param-value>【初始化参数值】</param-value>
	</init-param>
</filter>
<filter-mapping>
	<filter-name>【Filter别名】</filter-name>
	<url-pattern>【拦截路径】</url-pattern>
</filter-mapping>
```

#### FilterConfig类

web 工程启动的时候创建每个Filter对应的FilterConfig对象，并作为其init方法的传入参数

##### 常用方法

* getFilterName()
* getInitParameter(【初始化参数名】)

### 文件上传和下载

上传模板：

```java
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
	//只有是多段的数据，才是文件上传的
	if (ServletFileUpload.isMultipartContent(req)) {
		FileItemFactory fileItemFactory = new DiskFileItemFactory();
		ServletFileUpload servletFileUpload = new ServletFileUpload(fileItemFactory);
		try {
			// 解析上传的数据，得到每一个表单项 FileItem
			List<FileItem> list = servletFileUpload.parseRequest(req);
			// 循环判断，每一个表单项，是普通类型，还是上传的文件
			for (FileItem fileItem : list) {
				if (fileItem.isFormField()) {
					...
				} else {
					//读取文件
					String fieldName = fileItem.getFieldName();
					String name = fileItem.getName();
					fileItem.write(new File("url"));
					...
				}
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

下载模板：

```java
// 读取要下载的文件内容 (通过 ServletContext 对象可以读取)
ServletContext servletContext = getServletContext();
// 获取要下载的文件类型
String mimeType = servletContext.getMimeType("url");
// 在回传前，通过响应头告诉客户端返回的数据类型
resp.setContentType(mimeType);
// 还要告诉客户端收到的数据是用于下载使用
resp.setHeader("Content-Disposition", "attachment; filename=xxx");
// 把下载的文件内容回传给客户端
InputStream resourceAsStream = servletContext.getResourceAsStream("url");
IOUtils.copy(resourceAsStream,resp.getOutputStream());
```

### Cookie

Cookie类

常用方法

* new Cookie(key,value)
* getName()
* getValue()
* setValue()
* setMaxAge() 存活秒数。默认-1，负数表示浏览器一关Cookie 就会被删除（即session存活时间）；零表示马上删除 Cookie。
* setPath()作用于哪些路径

相关方法：

* request.getCookies()
* respond.addCookie(cookie)

### Session

HttpSession接口

常用于服务器端保存用户登录信息

常用方法：

* isNew()
* getId()
* setAttribute(key, value)
* getAttribute(key)
* setMaxInactiveInterval()超时秒数。默认30min；负数表示永不超时。
* invalidate()马上超时

相关方法：

* request.getSession()

### JSON

JavaScript Object Notation

一种轻量级的用于数据交换的文本格式。

格式：{"key":value,...}

java中引入第三方JSON类库后(Gson/Jackson)，可直接按照格式创建json对象并通过点运算符访问其中数据。

* JSON.stringify() 把 json 对象转换成为 json 字符串
* JSON.parse() 把 json 字符串转换成为 json 对象
* gson.toJson()把类对象转换为json 字符串
* gson.fromJson(JsonString, xxx.class)把json 字符串转换为类对象
