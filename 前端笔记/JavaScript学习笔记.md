# JavaScript学习笔记

（基于学过c&cpp&python&java）

> 主要参考资料
>
> 1. 尚硅谷:JS入门到精通(bilibili)
> 2. 尚硅谷:java web零基础入门完整版(bilibili)

## JavaScript语法基础

### 语言特性

- 动态语言
- 解释型（可由浏览器解析运行）
- 严格区分大小写
- 弱类型
- 交互性
- 安全性（不允许直接访问本地硬盘）
- 跨平台性

### 基本数据类型

1. string字符串型：使用单双引号
2. number数值型
3. boolean布尔型：只包括true和false
4. null型：本质是一个空对象(typeof(null)=Object)
5. undefined型
6. 其余为Object类（引用数据类型）

### 基本语法

- 注释：同c++
- ECMAScript 标识符采用驼峰命名法
- undefined==null:true
- 基本语法格式同c++
- 逻辑运算语句同c++，特殊的：`for(【变量】in 【对象】){}`随机顺序遍历对象所有可枚举属性，`for(【变量】of 【对象】){}`常用，避开for-in缺陷
- 算术运算符同c++，增加：`===`全等和 `!==`（相比 `==`和 `!=`不会发生类型转换）
- 栈保存变量（对象地址值）和基本类型数据，堆保存对象本身。

### 变量声明

- var 作用域为当前函数内，存在变量提升
- let 作用域为当前代码块内，不存在变量提升

var 声明变量默认初始化值为 undefined

### 作用域

scoping&hoisting

- js只有全局作用域和函数作用域，故想利用块级作用域需创建匿名函数 `(function () {【执行语句】}());`
- 变量提升：自动将变量的定义提升到函数顶部
- 函数提升：自动将函数的声明提升

### 标准库

- 转换为string：toString()、String()；转换为number：Number()、【字符串】.parseInt()、【字符串】.parseFloat()；Boolean()；
- `Infinity`、`NaN`
- `delete` 删除对象的属性等
- 基本包装类型类似java的包装类
- Math 对象

### Object类对象

- 定义初始化格式
  ```js
  法一：
      var 【变量名】 = new Object();
      【变量名】.【属性名1】 = 【属性值1】;
      【变量名】.【属性名2】 = 【属性值2】;
      ...
  法二：
      var 【变量名】 = {
          【属性名1】:【属性值1】,
          【属性名2】:【属性值2】,
          ...
      };

  ```
- 访问对象属性：`【对象名】.【属性名】`或 `【对象】['【属性名】']`
- constructor属性：引用了当前对象的构造函数
- 除了new还可用 `{}`返回一个空Object对象

### 数组

- 本质为Array对象
- 初始化：`new`或 `[]`
- 属性/方法
  - `length`
  - `indexOf(【元素】)`返回索引值

### 函数

- 本质是一个function对象
- 定义格式：`var 【函数名】 = function(【参数列表】){【执行语句】};`或 `function 【函数名】 (【参数列表】){【执行语句】};`
- 内部对象
  - arguments数组：用于保存函数的参数，内含属性callee表示当前函数
  - this 引用
- 构造函数定义格式：`function 【对象名】(【参数列表】) {this.【属性1】 = 【参数1】;【属性2】 = 【参数2】;}`
- 不支持重载，会直接覆盖

### 原型

- 构造函数中存在着一个名为原型的(prototype)对象，这个对象中保存着一些属性，凡是通过该构造函数创建的对象都可以访问
- 每一个对象都有原型，包括原型对象也有原型，除了Object的原型对象没有原型（实现继承）
- 如toString()函数存在于Object对应的原型中
- 访问方法：
  - `【构造函数】. prototype`
  - `【对象】._proto_`
  - `Object.getPrototypeOf(【对象】)`

### 输入输出

* alert()警告框输出
* console.log控制台输出

### 事件

#### 类型

* onload 加载完成事件： 页面加载完成之后，常用于做页面 js 代码初始化操作
* onclick 单击事件： 常用于按钮的点击响应操作。
* onblur 失去焦点事件： 常用用于输入框失去焦点后验证其输入内容是否合法。
* onchange 内容发生改变事件： 常用于下拉列表和输入框内容发生改变后操作
* onsubmit 表单提交事件： 返回布尔值来阻止表单提交，常用于表单提交前验证所有表单项是否合法。

#### 注册/绑定

静态注册：在js代码中定义函数，在html的标签中定义属性 `【事件类型】="【调用函数名】();"`

动态注册：在js代码中直接定义

```js
windows.onload=function(){
	var 【标签的dom对象】= document.getElementById("【id】");
	【标签的dom对象】.【事件类型】 = function(){...}
}
```

#### 事件对象

每触发一次事件，就会创建一个事件对象来记录此次触发事件的信息

事件函数的传入参数即为事件对象（常为even），可在事件函数内调用

#### 事件的冒泡

当父子标签对象同时绑定了同一个事件类型时，事件触发后会先调用子对象的相应事件函数，再调用父对象的相应事件函数，如此类推连锁传播。

##### 阻止方法

在子对象的相应事件函数内加上 `return false;`或 `event.stopPropagation();`

### DOM

Document Object Model 文档对象模型

把html文档中的标签、属性、文本，转换成对象来管理（整个文档是一个document对象），使用文档数的内存结构

#### 常用方法

* getElementById
* getElementsByName
* getElementsByTagName
* createElement
* appendChild

#### 常用属性

* childNodes
* firstChild
* lastChild
* parentNode
* nextSibling
* previousSibling
* className
* innerHTML起始标签和结束标签中的所有内容
* innerText起始标签和结束标签中的文本内容

### JQuery

用于查询的js库

JQuery对象可看作一个封装了多个DOM对象的数组

#### 核心函数$

##### 传入参数

* 函数：相当于window.onload = 函数
* html标签块：创建并返回这个标签块的JQuery对象
* 选择器：返回查询到的JQuery对象
* DOM对象：转换为JQuery对象返回

##### 选择器参数

###### 基本选择器

参数为单个选择器

###### 层级选择器

参数含两个选择器

* `【祖先选择器】 【后代选择器】`：匹配祖先节点下的后代节点
* `【父选择器】>【子选择器】`：匹配父节点下的子节点
* `【前置选择器】+【后置选择器】`：匹配前置节点后的相邻节点
* `【前置选择器】~【兄弟选择器】`：匹配前置节点的兄弟节点

###### 过滤器

参数中在选择器后缀过滤器

**基本过滤器**

* :first
* :last
* :not(selector)
* :even
* :odd
* :eq(index)
* :gt(index)
* :lt(index)
* :header
* :animated
  **内容过滤器**
* :contains(text)
* :empty
* :has(selector)
* :parent
  **可见性过滤器**
* :hidden
* :visible
  **属性过滤器**
* [attribute]
* [attribute =value]
* [attribute!=value]
* [attribute^=value]
* [attribute$=value]
* [attribute*=value]
* [attrSel1][attrSel2][attrSelN]
  **子元素过滤器**
* :nth-child
* :firstchild
* :last-child
* :only-child
  **表单过滤器**
* :input
* :text
* :password
* :radio
* :checkbox
* :submit
* :image
* :reset
* :button
* :file
* :hidden
  **表单对象属性过滤器**
* :enabled
* :disabled
* :checked
* :selected

#### JQuery和DOM加载页面的区别

* 执行顺序：浏览器解析完html文档的标签后，马上执行$( function(){} )，在加载完标签需要的资源后再执行window.onload = function(){}
* 执行次数：多个$( function(){} )顺序执行，多个window.onload = function(){}只会执行最后一个

#### JQuery对象方法

##### 元素过滤

* eq()
* first()
* last()
* filter(exp)
* is(exp)
* has(exp)
* not(exp)
* children(exp)
* find(exp)
* next()
* nextAll()
* nextUntil()
* parent()
* prev(exp)
* prevAll()
* prevUnit(exp)
* siblings(exp)
* add()
* serialize()将所有元素以"key=value&..."形式拼接返回

##### 属性操作

* html() 设置和获取起始标签和结束标签中的所有内容。
* text() 设置和获取起始标签和结束标签中的文本。
* val(字符串) 设置和获取表单项的 value 属性值
* val(字符串数组)设置选项按钮或下拉列表框的默认选择项
* addClass（）常用于添加样式
* removeClass（）常用于删除样式
* offset（）获取和设置元素的坐标。

##### DOM对象操作

* appendTo()
* prependTo()
* insertAfter()
* insertBefore()
* replaceWith()
* replaceAll()
* remove()
* empty()

##### 动作

可传参数有【时长】,【回调函数】等

* show() 将隐藏的元素显示
* hide() 将可见的元素隐藏
* fadeIn() 淡入（慢慢可见）
* fadeOut() 淡出（慢慢消失）
* fadeTo() 在指定时长内慢慢的将透明度修改到指定的值。

##### 事件

* blur()
* change()
* focus()
* click()
* mouseover()
* mouseout()
* scroll()
* submit()
* select()
* bind(type,fn)将函数绑定到一个或多个事件
* one(type,fn)将函数绑定到一个或多个事件但只一次

### AJAX 请求

Asynchronous Javascript And XML

是一种在js中异步向服务器发起请求，局部更新页面的技术。（浏览器地址栏不会发生变化）

常用模板：

```js
var xmlhttprequest = new XMLHttpRequest();
//设置请求方式、url、是否异步
xmlhttprequest.open("GET","url",true);
// 绑定 onreadystatechange 事件（每次readyState变化时会调用），处理请求完成后的操作。
xmlhttprequest.onreadystatechange = function(){
	if (xmlhttprequest.readyState == 4 && xmlhttprequest.status == 200) {
		var responseString = xmlhttprequest.responseText;
		...
	}
}
//发送请求
xmlhttprequest.send();
```

#### JQuery中的写法

##### $.ajax

```js
$.ajax({
	url:"",
	data:【路径参数（json格式）】,
	type:"【请求方式】",
	success:function (data) {
		var respondData = data;
		...
	},
	dataType : "【返回数据类型】"
});
```

##### $.get  \$.post

```js
$.get("url","【路径参数】",function (data) {...},"【返回数据类型】");

$.post("url","【路径参数】",function (data) {...});
```

##### $.getJSON

```js
$.getJSON("url","【路径参数】",function (data) {...});
```

END
