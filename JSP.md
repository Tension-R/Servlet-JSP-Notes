# JSP
## 1. 建立JSP
- JSP最终会变成一个完整的servlet在Web容器中运行。
- scriptlet就是放在<% ... %>标记中的Java代码。
- scriptelet代码会放在生成的servlet的服务方法中。
- 指令有3中：page、include、taglib

## 2. page指令
- 导入单个包：
		<% @ page import="..." %>
- 导入多个包，用逗号分离多个包。
- Java代码放在带百分号的尖括号中间，指令会为元素开始记号再增加一个字符@。
- page指令的属性：
	- import
	- isThreadSafe
	- contentType：定义JSP响应的MIME内容。
	- isElIgnored：定义转化页面时是否忽略EL表达式。
	- isErrorPage：定义当前页面是否是另一个JSP的错误页面，默认false，不能使用隐式的exception对象。
	- errorPage：定义一个资源的URL
	- language：定义scriptlet、表达式和声明中使用的脚本语言。现在可取值只有java。
	- extends；JSP变成servlet类后集成的类
	- session：定义页面是否有隐式的session对象，默认true。
	- buffer：定义隐式out对象如何处理缓存。
	- autoFlush：定义缓存的输出是否自动刷新输出，默认是true。
	- info：定义放到转换后页面中的串，这样能使用所生成servlet继承的getServletInfo()方法来得到这个信息。
	- pageEncoding：定义编码。

## 3. 表达式
- 表达式会为元素的开始记号增加一个字符：=。
- 表达式最后没有分号。
- 所有scriptlet中声明的变量总是局部变量。

## 4. JSP声明
- JSP声明用于声明所生成servlet类的成员，变量和方法都可以声明。
- JSP声明会为元素的开始记号增加一个字符：！
- JSP声明的所有内容都会增加到类中，并且置于服务方法之外。
- 可以声明静态变量和方法。

## 5. JSP隐式对象
- out------JspWriter
- request
- response
- session
- application------ServletContext
- config------ServletConfig
- exception(只有指定的错误页面才能用这个隐式对象）
- pageContext------PageContext
- page------Object
- 可以覆盖jspInit方法。
- 可以在配置文件中配置jsp初始化参数。

## 6. JSP中的属性
- JSP会使用4个隐式对象之一来得到和设置对应JSP中4个属性作用域的属性：
	- 应用：application
	- 请求：request
	- 会话：session
	- 页面：pageContext
- 可以使用PageContext引用来得到任意作用域的属性。
- PageContext类中保存着作用域常量。
- findAttribute方法用来查找一个属性。
- findAttribute会现在页面上下文查找，如果没有，就会先在请求作用域查找，再查找会话作用域，最后查找应用作用域，找到就截止。

## 7. taglib指令
- 定义JSP可以使用的标记库。

## 8. include指令
- 定义在转换时增加到当前页面的文本和代码。用来增加重复使用的代码。