# 无脚本的JSP
## 1. JavaBean标准动作
### 1. `<jsp:useBean>`和`<jsp:getProperty>`
- `<jsp:useBean>`标签用来声明和初始化在`<jsp:getProperty>`标签中使用的具体的bean对象。
- `<jsp:useBean>`声明初始化一个bean属性时，要声明id，class，scope。
- `<jsp:getProperty>`得到bean属性时，要有name和property属性值。
- `<jsp:useBean>`还可以创建一个bean。
- 可以使用`<jsp:setProperty>`设置一个属性值。
- `<jsp:useBean>`可以有体，可以把设置方法放在体内。
- 体中的代码会有条件的运行，只有找不到bean而且创建一个新bean时才会执行。
- type属性可以是class类型，抽象类型或者借口，只要能作为bean对象class类型的声明引用类型。class必须时type的一个子类或者具体实现。
- 如果使用type，没有class，bean必须已经存在。
- 如果使用了class，class不能是抽象类，而且必须有一个无参数的构造函数。
- scope默认属性为page。
- type == 引用类型（可以抽象）
- class == 对象类型（必须具体）
- 脚本可以放在标准动作内部。

### 2. 性质和请求参数
- param属性可以把bean的性质值设置为一个请求参数的值。
- 如果请求参数名与bean性质名匹配，就不需要在`<jsp:setProperty>`标记中为该性质指定值。
- 如果所有请求参数名与bean性质名匹配，可以把property设置为`*`自动匹配所有性质。
- Bean标记会自动转换String或基本类型的性质。
- 使用脚本时不会完成自动转换。

## 2. EL表达式
- 打印嵌套性质使用EL表达式非常容易。
- EL表达式总是放在大括号里，而且前面有一个美元符前缀：`${...}`
- 表达式的第一个命名变量可以使一个隐式对象，也可以是一个属性。

### 1. 点号操作符
- 如果表达式中变量后面有一个点号，点号左边的变量必须是一个Map或bean。
- 点号右边必须是一个Map键或一个bean的属性。
- 除pageContext隐式对象是一个bean，其他都是Map。
- 如果不能用作为Java代码中的变量名，就不能放在点号后面。

### 2. []操作符
- 使用[]时，左边可以是List或数组，右边可以是一个数，或者解析为一个数。
- 中括号里可以是Map键，可以是bean性质，也可以是数组或list的索引。
- 数组和List中的String索引会强制转换为int
- 对于bean和Map，这两个操作符都可以用。
- 如果中括号中不是String直接量，就会计算。
- 在中括号中可以使用嵌套表达式。

### 3. EL隐式对象
- pageScope
- requestScope
- sessionScope
- applicationScope
- param
- paramValues
- header
- headerValues
- cookie
- initParam
- pageContext
- 使用requestScope对象，可以把属性名放在引号中。

## 3.EL函数
- 函数方法必须是公共、静态的。
- 需要编写标记库描述文件（TLD）。
- 在JSP中放一个taglib指令。
- taglib指令中的uri要和配置文件中的uri匹配。
- EL能友好地处理null，算术表达式中看做0，逻辑表达式中看做false。

## 4. 布局模板
### 1. include指令
- `<%@ include file="***" %>`

### 2. `<jsp:include>`标准动作
- `<jsp:include page="***"`/>
- 内部原理并不相同。include指令在转换时发生。标准动作在运行时发生。
- include指令相当于把目标JSP内容复制到本JSP中。
- include标准动作会在运行时插入目标JSP的响应。

## 5. 使用`<jsp:param>`定制包含的内容
- 在include标准动作中使用`<jsp:param>`

## 6. `<jsp:forward>`标准动作
- 可以从一个JSP转发到另一个JSP，或者从一个JSP转发到一个servlet，还可以从一个JSP转发到Web应用中的任何其他资源。
- 尽量少使用，视图就是视图，控制逻辑交给控制层。
- 发生转发时，请求转发到的目标资源首先会清空响应缓存区。