#### 1、js的基本数据类型和引用数据类型

es6中新增了symbol，它的数据是唯一的，一般用来做对象的键

​	Number String boolean Undifined null symbol 

​	引用数据类型  Object  Array  Function Date Regexp

基本的数据类型存储在栈中，复合的数据类型数据存储在堆中，在栈中存储的是索引。而在堆中存储的复合数据类型有深拷贝和浅拷贝。浅拷贝就是将索引复制出一份，开辟一个新的栈空间来存储，两个索引指向的是同一个空间。深拷贝就是将堆中的数据复制一份，在栈中开辟一个新空间来存储，两个数据就不在有关系了。

#### 2、数据类型的判断

1. ​	typeof   对于基本数据类型判断是没有问题的，但是遇到引用数据类型（如：Array）是不起作用
2. instanceof	判断 new 关键字创建的引用数据类型，不考虑 null 和 undefined（这两个比较特殊）以对象字面量创建的基本数据类型
3. constructor   完全可以应对基本数据类型和引用数据类型 但如果声明了一个构造函数，并且把他的原型指向了 Array 的原型，这种情况下，constructor 也会力不从心
4. Object.prototype.toString.call()	完美的解决方案
5. jquery.type()如果对象是undefined或null，则返回相应的“undefined”或“null”。


#### 3、常用的字符串数组的方法

​	push、pop、unshift、shift、forEach、filter、splice、findIndex、find、includes、sort

#### 5、原型、原型链

​	每个函数都有一个prototype（普特太婆）属性，被称为显示原型 

​	每个实例对象都会有`_ _proto``（普特）_ _`属性,其被称为隐式原型

​	每一个实例对象的隐式原型`_ _proto_ _`属性指向自身构造函数的显式原型prototype  

​	每个prototype原型都有一个constructor（坑死抓可特）属性，指向它关联的构造函数。 

原型链

​	获取对象属性时，如果对象本身没有这个属性，那就会去他的原型`__proto__`上去找，如果还查不到，就去找原型的原型，一直找到最顶层(`Object.prototype`)为止。Object.prototype对象也有proto属性，值为null。 

#### 6、闭包

闭包概念：内部函数访问外部函数的变量，这种函数嵌套函数的形式

​		优点： 外部函数的变量会存储在内存中，可以避免全局变量的污染

​		缺点： 容易造成内存泄露，每调用一次都会产生一个新的闭包 

#### 7、作用域链

​	一段代码起作用的范围 分为全局作用域和局部作用域

函数内部使用变量，先从当前函数查找，如果找不到，则继续向父级查找，如果还找不到继续往上一级查找，最后找到window对象，如果还找不到，则报错提示变量不存在，这种链条关系就是作用域链

#### 8、HTTP Code

1xx：代表请求已被接受，需要继续处理

2xx：代表请求已成功被服务器接收、理解、并接受

3xx：被请求的资源必须通过指定的代理才能被访问

4xx：请求错误

5xx：服务器错误



#### 8、事件

1、js事件绑定的方式有三种：

1. 在DOM元素中直接绑定事件
2. 在Script代码中获取节点然后绑定事件
3. 用 addEventListener() 或 attachEvent() 来绑定事件监听函数

2、addEventListener()事件监听函数的第三个参数默认false是冒泡 改为 true是捕获

3、vue和原生js阻止事件冒泡的方法是 e.stopPropagation()  和事件修饰符.stop()

4、事件委托

​	事件委托就是事件代理，把子元素的响应事件比如click委托给父元素，让父元素担当事件监听的职务

​	如何实现：可以用jquery里的$.on  和  js里的addEventListener()事件监听的捕获阶段

​	好处：1、减少内存消耗

​				2、动态绑定事件

​	

#### 9、深拷⻉浅拷⻉的区别？如何实现⼀个深拷⻉？

浅拷贝（shallowCopy）只是增加了一个指针指向已存在的内存地址，

 深拷贝（deepCopy）是增加了一个指针并且申请了一个新的内存，使这个增加的指针指向这个新的内存，

 使用深拷贝的情况下，释放内存的时候不会因为出现浅拷贝而释放同一个内存的错误。

使用object.assgin和json的一些方法实现深拷贝

#### 10：for...in 迭代和 for...of 有什么区别

1、循环对象属性的时候使用 for...in，在遍历数组的时候的时候使用for...of。

2、for...in 循环出的是 key，for...of 循环出的是 value

3、for...of 不能循环普通的对象，需要通过和 Object.keys()搭配使用

#### 11：说一下从输入 URL 到页面加载完中间发生了什么?

\1. DNS 解析

\2. TCP 连接

\3. 发送 HTTP 请求

\4. 服务器处理请求并返回需要的数据

\5. 浏览器解析渲染页面

\6. 连接结束

#### 12： Object.defineProperty()方法有何作用

在对象上定义一个新属性，因为vue.js是采用`数据劫持`结合`发布者-订阅者模式`的方式，通过`Object.defineProperty()`来劫持各个属性的`setter`，`getter`，在数据变动时发布消息给订阅者，触发相应的监听回调来渲染视图

#### 13：ajax

ajax并不是一门新的技术，而是由 html css xml 和异步的js 等技术的组合，实现的是异步请求数据。

ajax的原理是由客户端请求ajax引擎，由ajax引擎请求服务器，服务器处理完数据后将结果返回给ajax引擎，然后 ⽤ JavaScript 来操作 DOM ⽽更新⻚⾯。ajax引擎的核心对象是XMLHttpRequest

ajax的实现方式有原生、jquery简化后的还有axios也可以

#### 14、跨域

域名的概念：ip地址的别名，域名和ip地址的关系就像人和面具

跨域是浏览器的安全策略，只有同域名 同端口号 同协议ajax才能访问，域名不同  端口号不一样 协议不一样就会跨域

用jsonp、cors、proxy解决跨域

**jsonp与json**

​	json是一种实现数据交换的轻量级的数据格式

​	JSONP(JSON with Padding)是[JSON](https://baike.baidu.com/item/JSON)的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题

​	jsonp的原理：script 的srcs属性不受同源策略的限制。



#### 15、h5、c3新特性

**h5：**

​	语义化标签：header、nav、section、aside、footer

​	音频audio 和视频video 

​	sessionStorage、localStorage

**c3：**

​	圆角：border-radius、盒子阴影 : box-shadow、盒子模型: box-sizing、背景:background-size、过渡动画 : transition 、自定义动画 animate、2D转换;transform: translate、3D转换：transform: translate3d

#### 16、防抖、节流

防抖：触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间

节流：高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率

#### 17、 Javascript如何实现继承?

JS继承实现⽅式也很多，主要分ES5和ES6继承的实现 

ES5三种⽅法 

⼀是原型链继承：即 B.prototype=new A() 

⼆是借⽤构造函数继承(call或者apply的⽅式继承)

组合继承是结合第⼀种和第⼆种⽅式

ES6继承是⽬前主流的继承⽅式，⽤class定义类，⽤extends继承类，⽤ super()表示⽗类

#### 18.说说new操作符具体⼲了什么？

1、创建一个空对象

2、设置原型链

3、让函数中的this指向对象，并执行函数体。

4、判断函数的返回值类型：

如果是值类型，返回obj。如果是引用类型，就返回这个引用类型的对象。

#### 19、谈谈this对象的理解？

- this对象总是指向函数的调用者
- 如果有new关键字，this指向new出来的那个对象
- 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象的window

### HTML

###### 1、BFC的理解？

理解:块级格式化上下文

原理：1.内部的盒子会在垂直方向一个接一个地放置，垂直方向的边距会发生重叠

​			2.BFC的区域不会与float区域的盒子重叠

​			3.计算BFC高度的时候,浮动元素也会参与计算

​			4.BFC是页面上独立的容器,外面的元素不会影响bfc里的元素,里面的元素也不会影响外面的

触发BFC

​		1.浮动元素，float 除 none 以外的值

​		2.定位元素，position（absolute，fixed）

​		3.display-inline-block

​		4.overflow-hidden，-auto，-scroll

2、说说你对盒模型的理解

盒模型就是把浏览器里的标签都看成⼀个矩形盒⼦，每个盒⼦都由:内容、边框、内边距、外边距四部分组成.

盒模型分为,标准盒模型和怪异盒模型

区别：  标准盒模型的宽高只包含内容，不包含其他部分
             怪异盒模型的宽高包含了内容、内边距和边框部分

通过box-sizing属性设置盒模型

###### 3、em/px/rem/vh/vw区别?

​	px：绝对单位，⻚⾯按精确像素展示

​	em：相对单位，相对于⽗节点的字体⼤⼩

​	rem：相对单位，相对根节点 html 的字体⼤⼩来计算

​	vh、vw：主要⽤于⻚⾯视⼝⼤⼩布局，在⻚⾯布局上更加⽅便简单

