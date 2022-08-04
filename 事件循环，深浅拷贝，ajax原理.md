**《--事件循环event loop--》**
js是单线程运行的，同一时间只能做一件事情，这是因为js是浏览器脚本语言，当我们执行js代码的时候，
浏览器会将我们同步的任务放在主线程中去执行，将异步的任务放到任务列表中，任务列表中又分为
宏任务和微任务，宏任务先入后出，微任务后入先出，执行时微任务比宏任务先执行，
宏任务中包含(定时器，ajax,dom事件)，微任务(promise,async,await,axios),promise中的.then是异步操作，
因为他在等待成功或者失败结果的返回，当我们执行时，先执行主线程中的数据，如果主线程中的数据全部执行
完毕了在去到任务列表中拉数据来执行，先执行微任务中的，微任务中的执行完返回结果后在执行宏任务中的数据
《--call apply bind区别--》应用场景继承父类中的属性
call apply bind都是改变this指向的,call传的是对象，apply传的是参数组，  bind返回改变this指向的一个函数需要调用才能执行 
obj.call(任意对象,多个参数)    obj.apply(任意对象,[多个参数])
call apply 改变this指向的原理是给原型中添加一个方法，这个方法this的指向，执行这个方法，然后再删除,传参是对应的
三者都可以改变函数的 this 对象指向
三者第⼀个参数都是 this 要指向的对象，如果如果没有这个参数或参数为 undefined 或 null ，
则默认指向全局 window
三者都可以传参，但是 apply 是数组，⽽ call 是参数列表，且 apply 和 call 是⼀次性传⼊参
数，⽽ bind 可以分为多次传⼊
bind 是返回绑定this之后的函数， apply 、 call 则是⽴即执⾏

面试题：1.用字面量方式创建2个对象，要求分别为两个对象添加方法，并用call()\applay() 实现互相调用方法
            var cat={
                name:'小猫'
                eat:function(food){
                    console.log(this.name+'爱吃'+food)
                }
            }
            var dog={
                name:'小狗',
                eat:function(food){
                    console.log(this.name+'爱吃'+food)
                }
            }
            cat.eat('鱼') //小猫爱吃鱼
            cat.eat.apply(dog,['鱼'])  //小狗爱吃鱼 通过apply改变cat的this指向，指向dog
            dog.eat('骨头') //小狗爱吃骨头
            dog.eat.call(cat,'骨头') // 小猫爱吃骨头  通过call改变dog的this指向，指向cat
《--合并对象  浅拷贝  深拷贝--》

合并对象的方法：1.for in 遍历循环进行赋值，
 2.  可以通过es5中object.assign()合并对象
        var a={a1:1};
        var b={a2:1};
        var c={a3:1};

         var obj=Object.assign(a,b,c)  //使用这个方法，目标对象也会改变  浅拷贝
        console.log(42,obj);       //数据覆盖了
        // console.log(a);   目标对象a自身也发生了改变


        var obj1=Object.assign({},a,b,c)
        console.log(50,obj1);
        console.log(51,a);  //目标对象不会发生改变

3.    展开运算符...
       var obj3={...a,...b,...c}     //数据覆盖了
       console.log(55,obj3);


        // 浅拷贝
        // 方法:Object.assign(), es6中的展开运行符{...a,...b},  for in 遍历对象，进行单层赋值
        // 特点：只拷贝一层
    如果属性是基本类型，拷⻉的就是基本类型的值。如果属性是引⽤类型，拷⻉的就是内存地址
    即浅拷⻉是拷⻉⼀层，深层次的引⽤类型则共享内存地址


        // 深拷贝 不能拷贝正则RegExp，data,error,undefined
        // 方法：JSON.parse(JSON.stringify(obj))   递归 
        // 特点：可复制多层，创建一块新的内存地址来存放复制的对象
        深拷⻉开辟⼀个新的栈，两个对象属完成相同，但是对应两个不同的地址，修改⼀个对象的属性，不会改变另⼀个对象的属性


for (const key in obj2) {
	//如果对象里还有对象，也就是多层？先判断是不是对象,是的话在次循环遍历赋值
	if( obj2[key] instanceof Object){
                for (const key1 in obj2[key]) {
		obj1[key][key1]=obj2[key][key1]
		}
	}
	//如果是一层直接赋值
	else{
		obj1[key]=obj2[key]
	} 
}
        console.log(105,obj1); 
基本类型数据保存在在栈内存中
引⽤类型数据保存在堆内存中，引⽤数据类型的变量是⼀个指向堆内存中实际对象的引⽤，存在栈中


《--原生ajax请求--》

AJAX 全称(Async Javascript and XML) 即异步的 JavaScript 和 XML ，是⼀种创建交互式⽹⻚应⽤
的⽹⻚开发技术，可以在不重新加载整个⽹⻚的情况下，与服务器交换数据，并且更新部分⽹⻚
Ajax 的原理简单来说通过 XmlHttpRequest 对象来向服务器发异步请求，从服务器获得数据，然后
⽤ JavaScript 来操作 DOM ⽽更新⻚⾯
实现 Ajax 异步交互需要服务器逻辑进⾏配合，需要完成以下步骤：
1.创建 Ajax 的核⼼对象 XMLHttpRequest 对象
2.通过 XMLHttpRequest 对象的 open() ⽅法与服务端建⽴连接
3.构建请求所需的数据内容，并通过 XMLHttpRequest 对象的 send() ⽅法发送给服务器端
4.通过 XMLHttpRequest 对象提供的 onreadystatechange 事件监听服务器端你的通信状态
5.接受并处理服务端向客户端响应的数据结果
6.将处理结果更新到 HTML ⻚⾯中

概念:是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术
1.实例化一个aa异步对象   var  aa=new XMLHttpRequest()
2.与服务器建立请求连接     aa.open("get(请求的东西在url中会显示)/post(请求方式)","url地址","异步请求(true)或同步请求(false),默认是异步请求")
3.发送请求   aa.send()
4.发送是否成功，如果成功后台服务器进行响应
前台请求状态事件onreadystatechange
aa.onreadystatechange=function(){
	前台请求状态readyState,一共有五种状态:0.初始化，1.连接上，2.已发送，3.请求处理中，4请求成功
	if(aa.readyState==4){
		后台服务器响应状态status，如果状态码为200的时候是响应成功，请求成功就返回内容，响应内容，如果请求失败就输出状态码
	}

}












































































































