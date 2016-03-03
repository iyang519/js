# js书籍阅读
### js启示录知识点总结

> 建议仔细阅读第一章和第八章，以及回顾内容

1.js构造函数构建并返回对象实例
* new+构造函数，该函数this值设置为正在构建的新对象，该函数默认返回this

2.js原生对象构造函数(9个)
* Number()
* String()
* Boolean()
* Object()
* Array()
* Function()
* Date()
* RegExp()
* Error()

注意：Math对象是一个静态对象，不是构造函数，不能var x = new Math()。Math只是一个由js设置的对象命名空间，用于存储数学函数

3.使用new操作符就是告诉js解释器，需要一个对应于构造函数实例对象

4.字面量
对于字符串，数字和布尔值使用字面量时，只有在该值被视为对象的情况下才会创建实际的复杂对象。
例如var charactersInfoo = 'foo'.length js会在字面量值创建一个一个包装器对象，调用这个方法以后，js即抛弃包装器对象，该值返回字面量类型

5.原始值和复杂值
* 5，'foo'，true，false，null，undefined等js值都被视为原始值，因为它们是不可细化的
* 原始值比较是值比较
* 复杂对象的比较是采用引用比较
* 原始值的复制是存储了值的副本，是真实值的复制
* 复杂值是引用进行存储和操作的，即通过内存的引用地址获取该对象的值

6.typeof 输出值需要注意
* typeof null  --  object
* typeof undefined  --  undefined
* typeof function(){}  -- function
* typeof new RegExp() -- function

7.构造函数实例都拥有指向构造函数的Construtor属性

8.验证对象是否有特定的构造函数的实例 instanceof

9.用点表示法或中括号表示法获取/设置/更新对象属性，一般使用点表示法，但是对于数字和保留关键字用作属性名称只有中括号可以访问他们
> var myobject = {'class':'foo'};console.log(myobject['class']);


10.删除对象的属性
<pre><code> var foo = { bar : "bar"};delete foo.bar;</code></pre>
delete不会删除在原型链上找到的属性，delete是将属性从一个对象中删除的唯一办法，将属性设置为undefined或null只是改变了属性的值，而不是将属性从对象中删除

11.使用hasOwnProperty验证对象属性不是来自原型链的。使用in操作符检查一个对象是否包含给定属性，不仅可以检查包含在引用对象中的属性，而且能够检查对象通过原型链继承的所有属性。

12.使用for in循环枚举对象属性
<pre><code>var cody = {
	age : 23,
	gender : 'male'
}
for (var key in cody){
	if(cody.hasOwnProperty(key)){
		console.log(key);
	}
}</code></pre>


13.Object()属性和方法
* constructor
* hasOwnProperty()
* isPrototypeOf()
* toLocaleStrinf()
* toString()
* valueOf()

14.使用对象字面量创建Object()。对象，没有必要将属性指定为字符串，除非属性名是以下几种情况：保留关键字，包含空格或特殊字符，以数字开始


15.Function对象实例属性和方法
* arguments 是一个类数组对象，包含所有传递给函数的参数
arguments.callee属性，它是对当前执行函数的引用，在函数需要递归调用，它非常有用
<pre><code>var foo = function foo(){
	console.log(arguments.callee);//输出foo()
}</code></pre>
*constructor

length 实际上可以获取函数所需要参数总数量
<pre><code>var myFunction = function(z,s,d,e,r,m,q){
	return myFunction.length;
}
console.log(myFunction());//7</code></pre>

* apply()、call() 
apply和call的区别在于参数传递不同，前者是传递传递多个参数组成的数组，后者多个分开的参数

* toString()

16.在js中，函数是对象，意味着函数可以存储在一个变量，数组或对象中，函数可以传递给函数，并由函数返回，函数可以拥有属性，因为它是一个对象。

17.传递给所有函数的this关键字都是对包含函数对象的引用。作为属性包含在对象内的函数，可以用this来获得对‘父’对象的引用（使用new关键字或apply(）call()除外)在new中this值引用实例本身，原型方法内的this关键字引用构造函数实例。当函数在全局作用域定义时，this值为全局对象。
*注意：当this值得宿主函数被封装在另一个函数的内部或在另一个函数的上下文被调用时，this将永远对head对象的引用，简单的在父函数中使用作用域链来保留对this的引用，以便this值不丢失。
<pre><code>var myObject = {
	func1 : function(){
		console.log(this);//myObject
		var that = this;
		var func2 = function(){
			console.log(this);//head对象
			console.log(that);//myObject
		}
    }
}</code></pre>

18.函数提升，在运行代码之前，函数语句已经被编译器解释，并添加到执行堆栈/上下文，在使用函数语句要确保自己明白这一点
<pre><code> var speak = function(){
	sayYo();//输出yo
	funtion sayYo(){
		console.log('yo');
    }
}</code></pre>

19.head对象是js环境中可用的最高作用域/上下文，在web浏览器中有以下方法
* decodeURI()
* decodeURIComponent()
* encodeURI()
* encodeURIComponent()
* eval()
* isFinite()
* isNaN()
* parseFloat()
* parseInt()

20.作用域有三种类型，全局作用域，局部作用域，和eval作用域。

21.js没有块作用域，只有函数，全局，eval作用域。由于if，for无法创建作用域，因此变量可以变相覆盖。

22.作用域链查找返回第一轮值。

23.函数定义确定作用域，而非调用确定。因此我们可以创建闭包，我们可以让函数向全局作用域返回一个嵌套函数，但该函数能够通过作用域链访问父函数的作用域。

24.数组对象实例属性和方法
* 属性：constructor,index,input,length
* 方法：pop(),push(),reverse(),shift(),unshift(),sort(),splice(),concat(),join(),slice()

25.遍历数组最简单的方法就是while循环
<pre><code>var myArray = [];
var myArrayLength = myArray.length;
while(myArrayLength--){
	...;
};</code></pre>
不用for循环是因为while循环参数很少，更容易阅读

26.使用null显示指出对象属性不包含值，typeof(null)===object。验证null值总是使用===，使用==无法区分undefined和null；

27.undefined 一种表示声明变量没有指定值，一种表示访问对象的属性没有被定义，且不在原型链。

28.全局作用域内定义的函数和变量没有使用var会成为全局对象的属性，使用var会成为全局变量。


29.Function()构造函数为每个实例赋一个prototype属性。默认prototype属性是object对象。

30.将构造函数创建的实例链接至构造函数的prototype属性


### 编写可维护的JavaScript
> 建议认真阅读第七章事件处理，第十章抛出自定义错误，以及第三部分自动化

1.代码缩进层级-4个空格字符

2.语句结尾-不要省略分号

3.一行长度限定在80个字符，多行字符可以用拼接符 + 来将字符串分成多份

4.在运算符换行后，第二行追加二个缩进，运算符（类似 , && + 等）应该作为前一行的行尾。

5.命名采用驼峰法大小写命名。不建议使用匈牙利命名法

6.变量命名前缀应该是名词，方法是动词前缀。例如count,length,size表示数据类型，getName就是函数命名

7.常量是大写字母加下划线

8.单行注释和多行注释之前应该有一个空行，且缩进。添加注释的原则是让代码更清晰。此外还有文档注释

// 单行注释

/*
 *
 * 多行注释
 */

/**
文档注释
@method
@param
@return 
**/

9.if for while do...while... try...catch... 所有块语句都应该使用花括号

10.流行的写法是将所有变量声明放在函数顶部，而不是散落在各个角落
var value = 10,
    i,
    len;

11.先声明函数然后在使用函数，且函数声明不应该出现在语句块之内

12.最好不要在全局作用域使用"use strict"
<pre><code>(function(){
	"use strict";
})()</code></pre>

13.推荐使用===和!==，不推荐使用==和!=

14.减少使用eval()和Function()，且减少给setTimeout() setInterval()传入字符串参数


15.UI层解耦，将JavaScript，css，html相互抽离。
将javascript从css抽离典型例子，避免使用css表达式
将css从JavaScript抽离典型例子，用className成为js和css通信桥梁
将JavaScript从html抽离典型例子，避免将脚本嵌入到html中运行
将html从JavaScript抽离典型例子，模板引擎

16.避免使用全局变量
*单全局变量方式，将所有功能代码都挂载在全局对象上，例如jquery定义了二个全局对象$和jQuery。
*命名空间是简单的通过全局对象的单一属性表示功能的分组。
*异步模块定义AMD
*零全局变量，如果你的脚本较短，也不需要交互，可以考虑使用零全局变量方式来实现
<pre><code>(function(win){
	
}(window))</code></pre>

17.避免变量与null的比较。如果检测null则直接使用恒等运算符 === 或非恒等运算符 !==


18.typeof运算符将用于一个未声明的变量也不会报错，未定义的变量和值为undefined的变量通过typeof都返回undefined。


19.在检测自定义类型时，最好做法是使用instanceof运算符。
<pre><code>function Person(name){}
var me = new Person('renyang');
console.log(me instanceof Person);</code></pre>

20.检测函数最好的方法是使用typeof。
<pre><code>function myFunc(){} console.log(typeof myFunc === "function");//true</code></pre>

21.检测数组方法
<pre><code>function isArray(value){
	return object.prototype.toString.call(value) === "[object Array]";
}</code></pre>

22.检测属性是否存在
不好写法
* if(object[propertyName]){} 
* if(object[propertyName] != null){}
* if(object[propertyName] != undefined){}
判断属性是否存在的最好方法是使用in运算符，in运算符仅仅简单的判断属性是否存在，而不会读属性的值
只是想检测实例对象的某个属性是否存在，则使用hasOwnProperty()方法。
好的写法：
if(object.hasOwnProperty('related')){}

23.将配置数据从代码中分离出来

24.不是你的对象不要动

25.delete操作符只能对实例的属性和方法起作用，如果在prototype属性和方法使用delete是不起作用的，但是仍可以用对其赋值为null的方法来阻止被调用。

26.throw new Error('something bad happened!');
抛出包含任何你需要的有助于调试问题的信息。针对所有浏览器，唯一不出差的显示自定义错误消息的方式就是用一个Error对象。


27.何时抛出错误，由于js没有类型或参数检查，要充分进行类型检查。

28.try{}catch(ex){} 当try模块发生了一个错误时，程序立即停止执行，然后跳到catch块，并传入一个错误的对象。



