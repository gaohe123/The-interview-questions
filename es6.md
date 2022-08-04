#### 1、es6新增了let和const关键字

- ​	let和var的区别

  1. let只在代码块中有效{}，var是全局的
  2. var存在变量的提升，let没有
  3. let的变量不能重复定义

- ​    const是干什么用的

  ​	定义常量用的

#### 2、解构赋值（能举出简单的例子）

就是在数组或者对象中拿出自己想要的变量

```js
// let {data:res}=await this.$http.get("/data.json")
let {username}={"username":1,"age":2}
var [a,...b]=[1,2,3]
console.log(username)
console.log(a)
console.log(b)
```

#### 3、js的数据类型有些

- ​	基本数据类型

  ​	Number 、 String 、 Boolean   null 、undefined   Symbol

- ​    引用数据类型

  ​	Object  Array Function regExp Date

#### 4、怎么判断数据类型

1. ​	typeof  有什么问题出现了instanceof

   ​	typeof()检测基本数据类型除了null  undefined  

   ​		typeof(null)返回Object   

   ​		typeof(undefined) 返回undefined

2. ​    instanceof 有什么问题出现 constructor

   ​	在判断引用数据类型的时候  判断引用数据类型和Object返回的都是true

   ```
   console.log( arr instanceof Object) true
   console.log( arr instanceof Array) true
   ```

3. ​     constructor有什么问题出现 Object.prototype.toString()

   能解决instanceof的问题 但是解决不了  null和undefined 

   ```js
     var arr=[]
     console.log(typeof([]))
     console.log( arr instanceof Object)
     console.log(arr.constructor==Array)
     console.log(arr.constructor==Object)
   ```

4.    Object.prototype.toString.call(变量)最完美的解决方式

   ```
     console.log(Object.prototype.toString.call(arr))
   ```

#### 5、新增了箭头函数

​	箭头函数与普通函数的区别：

1. 普通函数存在着变量的提升，箭头函数没有
2. 普通函数的this指向，谁调用指向谁，箭头函数是在哪定义就指向谁
3. 普通函数可以当成构造函数，而箭头函数是不可以的
4. 箭头函数没有arguments,要接受所有的参数用...rest	

#### 6、字符串新增的方法

1. padStart 填充
2. includes  在大串中找到子串返回的是true  找不到返回的false

#### 7、需要掌握的数组方法

1. find()
2. findIndex()
3. filter()
4. includes

#### 8、模块化(演示只能爱webpack编译后才能看到，所以可以在工程化项目总演示)

​	模块就是独立的js文件，可以导出 函数，对象，字符串，数字，布尔值，类等

​	模块有导入与导出

​	**export与import**

​	抛出export {一堆东西}

​	接受是一个一个的接 import {接哪个写哪个 as 别名} from “文件”

```
var fun=function(){
    console.log('还不放假')
}
var username="孙佳乐"
export {username,fun}

import {username as user,fun}  from "@/http"
console.log(user)
fun()
```

​	**export default 与import**

​	接受和export不一样   接受的所有的东西都是一个整体

```
var fun=function(){
    console.log('还不放假')
}
var username="孙佳乐"
export default{username,fun}

import  obj  from "@/http"
console.log(obj.username)
obj.fun()
```

​	**modules.export与require**

​	抛出或者导入  遵循的规范是commonjs

​	需要要modules.export抛出，用require来导入

```
var fun=function(){
    console.log('还不放假')
}
var username="孙佳乐"
module.exports={username,fun}

var obj=require('@/http.js')
console.log(obj)
```



#### 9、promise

- 什么是同步 异步

  同步：在同一时间内只能干一件事情。体现程序中就是代码块B必须等待代码块A执行完毕后再执行

  异步：在同一时间内可以干多件事情。体现在程序中就是代码块B在执行的时候不用等着代码块A的结果

- es5是怎么实现异步的

  是通过回调的方式实现异步  然后回调的方式会有回调地狱的风险 

- es6是怎么实现异步的

  promise是es6解决异步放入一种解决方式

  promise是一个对象，在new这个对象的时候需要传递一个函数  这个函数有两个参数 分别为请求成功后的回调  请求失败后额回调

  promise有三种状态  正在进行  成功  失败

- promise是api有哪些

  then() 可以有一个回调函数  resolve 请求成功

  then()可以有两个回调   成功  失败

  catch()可以处理异常

  all()批量执行promise  Promise.all()都成功返回成功数组结果  有一个失败 总的就失败返回第一个失败的

  race()有一个成功就成功

- es7是怎么实现异步的	

- promise怎么处理错误

  1. then()的两个函数
  2. catch()

  

  获取网络数据的方式

  1、原生

  2、jquery简化后的ajax

  3、axios

  4、fetch

  5、vue-resource

  

#### 10.面向对象

- 关于面向对象的概念

  1. 面向对象和面向过程

     是一种编程的思维

     面向过程强调的是步骤 面向对象强调的是封装

  2. 什么是对象

     1. 万物皆为对象（笼统的概念）

        对象是具体的实例   实例是可以拿过来直接干活的

  3. 对象与类之间的关系

     类：具有相同的属性（特性 变量）和方法（能干啥啊）对象的集合

     一个类可以有n个对象  每个对象之间都是相互独立的

  4. 怎么创建对象

  5. 什么是继承

- es5怎么创建对象

  ```
  <script>
  //构造函数  实例化对象的时候需要传递三个参数
  function Person(name,age,classname){
    //属性的赋值
    this.username=name;
    this.userage=age;
    this.classname=classname
    //方法
  }
  Person.prototype.say=function(){
    console.log(this.username+"回家吧")
  }
  //构造函数解决了重复代码的问题  解决指向问题
  var obj1=new Person('xiaosan',18,"2104A")
  var obj=new Person("小四",19,"2104A")
  obj.say()
  console.log(obj1.say==obj.say)
  //给每一个实例的方法都分配一个空间 会造成空间的浪费
  //要的是构造函数和原型的混合模式 用构造函数的模式定义属性  用原型的模式定义方法
  </script>
  ```

- es6声明类是谁的语法糖

  es5 构造函数模式和原型模式的语法糖

-  es6创建对象的语法

  ```js
  <script>
  class Person{
    //每个类中都有一个构造函数 constructor 构造函数每次被new的时候被执行 如果没有定义就自动的创建一个没有任何参数 没有操作的构造函数 作用是属性赋值
    constructor(name,age,classname) {
        this.name=name
        this.age=age
        this.classname=classname
    }
    //静态属性  只能用类名调用
    static school="积云"
    //静态方法  只能类名
    static fun(){
      console.log('谁说的放假了')
    }
    //方法
    say(){
      console.log(this.name+"放假了")
    }
  }
  var obj=new Person("xiaosan",20,"2104A")
  var obj2=new Person("xiaosi",20,"2104A")
  console.log(obj.school)
  console.log(obj.say==obj2.say)
  Person.fun()
  </script>
  
  ```

- es6的继承

  如果好多子类有共同共同的特性和方法可以提取出来 做成一个父类，子类继承父类就能拥有父类的属性和方法

  

- es6面向对象案例

- 原型链

  当一个对象调用自身不存在的属性/方法时，就会去自己 [proto] 关联的前辈 prototype 对象上去找，如果没找到，就会去该 prototype 原型 [proto] 关联的前辈 prototype 去找。依次类推，直到找到属性/方法或 undefined 为止。从而形成了所谓的“原型链”。

