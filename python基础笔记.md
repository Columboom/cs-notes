# Python学习笔记
（基于学过c&cpp）


 > 主要参考资料
 > 1. 李巍-成都工业大学-2016级数字媒体专业实训课程-Python爬虫和数据可视化-2021Python爬虫编程基础5天速成（+数据分析)(bilibili)

## Python语法基础

#### 语言特性
- 基于c语言实现的
- 解释型（理解？）
- 开源
- 支持交互式
- 可跨平台移植
- 弱类型（自动匹配，定义变量无需指定数据类型）
- 所有数据类型均为引用？

#### 编译运行
- 边解释成机器码边运行，不需要之间文件
- cpython：自带的编译器，命令行进入python后，加上提示符为`>>>`即可调用
- python2和python3不兼容

#### 基本格式及其他
- 无需文件头和main函数入口，直接写顺序运行语句即可
- 源文件首行一般写上`#-*- coding:utf-8 -*-`或者`# coding=utf-8`以便于在代码中使用中文字符
- 在执行语句开头加入main函数信息可便于测试程序`if __name__ == "__main__" :`
- 每行语句后无需`;`结尾
- 无`{}`，以缩进划分语句块
- 注释
    - 单行：`#...`
    - 多行：`'''...'''`
- `非0`或`非空值`可表示`True`，`0`或`None`可表示`False`
- 区间表示通常为左闭右开
- `pass`占位空语句
- python3源码默认以UTF-8编码，即Unicode字符串
- 无`++`和`--`
- `del 【变量名】` 删除该变量（实质是解除引用而非删除对象），删除字符串、列表、元组元素后会自动补齐
- `【变量名】[【起始下标，默认开头】:【终止下标，默认末尾】:【步进，默认为1】]`切片，对字符串、列表、元组
- 可用`+`和`*【正整数】`拼接字符串或列表
- 字符串、列表、元组的元素均可用`[【下标】]`访问，字典元素用`[【key】]`访问

#### 模块导入
- 模块即py文件
- 在sys.path以及本文件目录中查找
- `import 【模块名】 `导入整个模块
- `from 【模块名】 import 【函数/类名1】(,【函数/类名2】...)`从模块中导入函数/类，`from 【模块名】 import \*`从模块中导入所有函数
- `from 【包名】 import 【模块名】`从包中导入模块
- `import【包名】.【模块名】`、`import【模块名】.【函数/类名】`
- 调用导入的函数`(【包名】.)【模块名】.【函数/类名】`

#### 输出输入
- 输出`print(...)`
- 输出内容用`,`号连接，输出时默认用空格分隔，可在print内自定义`sep="【分隔符】"`
- 输出内容末尾默认换行，可在print内自定义`end="【末尾符】"`
- 格式输出：`print("...%【转换说明符】..."%【变量名】)`，若有多个变量可用元组`%(【变量名1】,【变量名2】...)`
- 输入`input("【提示字符串】")`返回字符串类型

#### 标准库与函数
- `type()`返回数据类型
- `【数据类型】()`强制类型转换
- `id()`返回对象内存地址
- `random`随机库，内含`random()`、`randint(【最小整数】,【最大整数】)`等函数
- `range(【最小数，默认为0】, 【最大数】, 【步长，默认为1】)`可迭代对象
- `len()` 返回对象（字符、列表、元组等）长度或项目个数
- `hasattr(【对象名】,'【属性名】') `判断对象是否包含对应的属性
- `enumerate() `接受一个可遍历对象，同时返回元素下标和元素作为一个元组
    ```py
    seasons = ['Spring', 'Summer', 'Fall', 'Winter']
    list(enumerate(seasons))
    #list=[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
    list(enumerate(seasons, start=1))      
    #list=[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
    for i, element in enumerate(seq):
        ...
    ```

#### 运算符
- `**`幂运算
- `//`取整除
- `and`与
- `or`或
- `not`非
- `in`在序列中
- `not in`不在序列中
- `is`引用自同一个对象
- `is not`引用自不同一个对象

#### 基本逻辑语句
- 条件判断语句格式
    ```py
    if 【判断条件1】:
        【执行语句1】
    elif 【判断条件2】:#可选
        【执行语句2】
    ...
    else :#可选
        【执行语句n】
    ```
- 循环语句格式
    ```py
    for 【变量】 in 【可遍历对象如range()或字符串或列表】 :
        【执行语句】
    ```
    ```py
    while 【判断表达式】:
        【执行语句】
    else:#可选
        【执行语句】
    ```

#### 字符串
- 使用单引号或双引号或三引号（支持多行）
- 在字符串前加`r`表示字符串中不进行转义
- 字符串函数

#### 列表list
- `[【元素1】,【元素2】...]`
- 元素的数据类型可以不同，可嵌套
- 正负索引均可访问指定元素，`-1`表示末尾元素
- 列表函数

#### 元组tuple
- `(【元素1】,【元素2】...])`
- 可看作特殊的列表
- 元素不可修改
- 定义只有一个元素的元组时必须追加`,`号以区分

#### 字典dict
- `{【key1】:【value1】,【key2】:【value2】...}`或`dict([(【key1】,【value1】),(【key2】,【value2】)...])`
- key须用不可变类型
- `[]`访问不存在key会报错，常用`get(【key】,【不存在时返回值，默认为"None"】)`
- 字典函数

#### 集合set
- 可看作仅存key的字典
- 初始化`set(【列表】)`重复元素会被自动过滤

#### 函数
- 定义格式
    ```py
    def 【函数名】():
        【执行语句】
    ```
- 可有多个返回值
- 若想在局部范围访问全局变量，需声明`global 【全局变量名】`

#### 异常
格式
```py
try:
    ...
except (【异常类型1】,【异常类型2】...) as【储存捕获的异常信息字符串】:#as可选
    ...
 ```


 ## Python爬虫

 #### 基础知识及其他
 - url分析
 - chrome 开发者工具的使用
 - 访问url时浏览器与服务器第一次交互，浏览器提供Headers(主要有Rrespond headers、Cookies、Request headers)等，服务器返回Respond等
 - html文件框架

#### 正则表达式
- 常用操作符
   - `.`表示任何单个字符
   - `[]`字符集，对单个字符给出取值范围
   - `[^]`非字符集，对单个字符给出排除范围
   - `*`前一个字符次或无限次扩展
   - `+`前一个字符1次或无限次扩展
   - `?`前一个字符0次或1次扩展
   - `|`左右表达式任意一个
   - `{m}`扩展前一个字符m次
   - `{m, n}`扩展前一个字符m至n次(含n)
   - `^`匹配字符串开头
   - `$`匹配字符串结尾
   - `()`分组标记，内部只能使用|操作符
   - `\d`数字，等价于`[0-9]`
   - `\w`单词字符，等价于`[A-Za-z0-9_]`
 - 常用模板：... 

 #### bs4包的Beautifulsoup类  
 网页解析，获取数据
 - 构造函数`Beautifulsoup(【文件源码】,【解析器】)`如`bs=Beautifulsoup(html,"html.parser")`用于HTML文件时，将其转换成ー个树形结构，储存的结点是4种对象
    1. Tag对象：可通过`.【标签名】`访问html中的第一个对应的标签及其内容（）
    2. NavigableString对象：标签里的内容，可通过`.【标签名】.string`访问
    3. Beautifulsoup对象：自身
    4. Comment对象：特殊的NavigableString对象，但输出内容不包含注释
 - `.【标签名】.attrs`作为字典访问该标签的所有属性
 - `.【标签名】.contents`作为列表访问标签的所有内容
 - `find_all()`可选的传入参数
   - 字符串，返回含所有对应字符串的列表
   - 正则表达式，按正则表达式搜索
   - 函数，根据函数要求搜索
   - `【标签的参数】=【参数值】`，作为列表返回符合条件的所有标签及其内容
   - `text=【字符串】`作为列表返回内容与该字符串相同的标签的内容
   - `limit=【最大个数】`限定搜索返回的元素个数
   - 其他
 - `select()`css选择器查找 
   - 传入字符串，返回含所有对应字符串的列表
   - 传入`".【类名】"`，通过类名查找
   - 传入`"#【id值】"`，通过id查找
   - 传入`"【标签名】[【标签的参数】=【参数值】]"`，通过属性查找
   - 传入`"【父标签名】>【子标签名】"`，通过子标签查找
   - 其他

 #### re包
 用于正则表达式搜索
 - 函数
   - `compile(【包含正则表达式的字符串】,【re修饰符（可选）】)`创建并返回模式对象 （只会返回`()`中的正则表达式内容）
   - `search(【正则表达式/模式对象】,【待处理字符串】)`在一个字符串中搜索匹配正则表达式的第一个位置，返回 match对象
   - `match(【正则表达式/模式对象】,【待处理字符串】)`从一个字符串的开始位置起匹配正则表达式，返回 match对象
   - `findall(【正则表达式/模式对象】,【待处理字符串】)`搜索字符串，以列表类型返回全部能匹配的子串
   - `split(【正则表达式/模式对象】,【待处理字符串】)`将一个字符串按照正则表达式匹配结果进行分割，返回列表类型
   - `finditer(【正则表达式/模式对象】,【待处理字符串】)`搜索字符串，返回一个匹配结果的迭代类型，每个迭代元素是 match对象
   - `sub(【正则表达式/模式对象】,【替换字符串】,【待处理字符串】)`在一个字符串中替換所有匹配正则表达式的子串，返回替换后的字符串
 - re修饰符
   - `re.I`使匹配对大小写不敏感
   - `re.L`做本地化识别(locale-aware)匹配
   - `re.M`多行匹配，影响`^`和`$`
   - `re.S`使.匹配包括換行在内的所有字符
   - `re.U`根据 Unicode字符集解析字符，影响\w,\W,\b,\B
   - `re.X`给予更灵活的格式以便易于理解

 #### urllib.request&urllib.error
 制定URL，获取网页数据
 - `urlopen()`
   - 返回相应网页类的文件对象，内含html源码（文件read默认二进制返回，故最好后加`.decode('utf-8')`）
   - 获取get请求（相当于直接打开网址）：`【url字符串】`作参数
   - 获取post请求（常用于需要登录等交互打开的网址）：增加参数`data=bytes(urllib.parse.urlencode(【字典类型信息】),encoding=utf-8)`
   - 设定时间限制：增加参数`timeout=【秒数】`
   - http文件对象含包含了请求信息，如属性：status状态码、getheaders()返回Rrespond headers
   - `Request()`封装的请求信息作参数
 - `Request()`封装请求信息返回请求对象，参数可包括url=、method=（默认get请求）、data=（常用于上述获取post请求）、headers=【字典类型信息】（常传入Request headers伪装浏览器访问）
  

 #### xlwt包
 进行excel操作
 - `Workbook()`创建workbook对象
 - workbook函数：`add_sheet(【表单名】)`创建worksheet对象；`save(【文件名】)`保存excel文件
 - worksheet函数：`write(【行号】,【列号】,【数据内容】)`写入数据

 #### sqlite3包
 进行SQLite数据库操作
 - `connect(【数据库名（常为db文件】)`创建并打开数据库文件，创建并返回该文件的连接对象
 - connect函数
   - `cursor()`获取游标对象；游标函数`execut(【sql语句的字符串】)`执行sql语句
   - `commit()`提交对连接对象的所有操作给数据库文件
   - `close()`关闭连接对象
 ```py
     connect=sqlite3.connect("xxx.db")
     cursor=connect.cursor()
     #sql1 建表并初始化表头
     sql1='''
        create table 【表名】
         (【项名1】 【数据类型】 【其他修饰符】,【项名2】 【数据类型】 【其他修饰符】...);
     '''
     cursor.execut(sql1)
     #sql2 插入数据
     sql2='''
        insert into 【表名】(【项名1】,【项名2】...)
            values(【项1数据】,【项2数据】...);
     '''
     cursor.execut(sql2)
     #sql3 查询并获取数据
     sql3="select 【项名1】,【项名2】..."
     datalist=cursor.execut(sql3)
     
     connect.commit()
     connect.close()
 ```

 #### 爬虫基本步骤
 1. 爬取网页
 2. 解析数据
 3. 保存数据
 ```py
 import re
 import bs4
 import urllib.request,urllib.error
 import xlwt
 import sqlite3

 def askURL(url):
     headers={"User-Agent":"..."}
     req =urllib requestRequest(url, headers=headers)
     # htmlcode=""
     try:
        response =urllib.request.urlopen(req)
        htmlcode=response.read().decode("utf-8")
        # print(htmlcode)
     except urllib.error.URLError as e:
        if hasattr(e, "code"):
            print(e.code)
        if hasattr(e, "reason"):
            print(e.reason)
     return htmlcode

findxxx=re.compile(【包含正则表达式的字符串】,re.S)
 def getData(baseurl):
    datalist=[]
    for i in range(...):
        url=baseurl+...
        htmlcode=askURL(url)
        #解析数据
        bs=Beautifulsoup(htmlcode,"html.parser")
        for i in bs.find_all('div',class_="item"):
            data=[]
            i=str(i)
            xxx=re.findall(findxxx,i)[0]
            data.append(xxx)
    return datalist

 def saveDataXsl(datalist,savepathxsl):
     workbook=xlwt.Workbook(encoding="utf-8",style_compression=0)
     worksheet=workbook.add_sheet(【表单名】,cell_overwrite_ok=True)
     colhead=(...)#表头
     for i in range(0,itenum):
         worksheet.write(0,i,colhead[i])
     for i in range(0,datanum):
         for j in range(0,itenum):
             worksheet.write(i+1,j,datalist[i][j])
     workbook.save(savepathxsl)

  def initdb(dbpath):
     connect=sqlite3.connect(dbpath)
     cursor=connect.cursor()
     sql='''
        create table 【表名】
         (【项名1】 【数据类型】 【其他修饰符】,【项名2】 【数据类型】 【其他修饰符】...);
     '''
     cursor.execut(sql)
     connect.commit()
     connect.close()

 def saveDataSQL(datalist,savepathdb):
     initdb(savepathdb)
     connect=sqlite3.connect(dbpath)
     cursor=connect.cursor()
     for data in datalist:
         for i in range(len(data)):
             data[i]='"'+data[i]+'"'
         sql='''
            insert into 【表名】(【项名1】,【项名2】...)
            values(%s);
         '''%",".join(data)
         cursor.execut(sql)
         connect.commit()
     cursor.close()
     connect.close()

 def main():
     baseurl="..."
     datalist=getData(baseurl)
     savepathxsl="....xsl"
     saveDataXsl(datalist,savepathxsl)
     savepathdb="....db"
     saveDataSQL(datalist,savepathdb)
 
 if __name__ == "__main__" :
     main()

 ```

 ## 数据可视化
 #### Flask入门
 #### Echarts应用
 #### WordCloud应用