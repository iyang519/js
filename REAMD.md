js启示录

## js构造函数构建并返回对象实例
* new+构造函数，该函数this值设置为正在构建的新对象，该函数默认返回this

## js原生对象构造函数(9个)
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
5，'foo'，true，false，null，undefined等js值都被视为原始值，因为它们是不可细化的
原始值比较是值比较
复杂对象的比较是采用引用比较
原始值的复制是存储了值的副本，是真实值的复制
复杂值是引用进行存储和操作的，即通过内存的引用地址获取该对象的值

6.typeof 输出值需要注意
typeof null  --  object
typeof undefined  --  undefined
typeof function(){}  -- function
typeof new RegExp() -- function

7.构造函数实例都拥有指向构造函数的Construtor属性

8.验证对象是否有特定的构造函数的实例 instanceof

9.用点表示法或中括号表示法获取/设置/更新对象属性，一般使用点表示法，但是对于数字和保留关键字用作属性名称只有中括号可以访问他们
var myobject = {'class':'foo'};
console.log(myobject['class']);


10.删除对象的属性
var foo = { bar : "bar"};
delete foo.bar;
delete不会删除在原型链上找到的属性，delete是将属性从一个对象中删除的唯一办法，将属性设置为undefined或null只是改变了属性的值，而不是将属性从对象中删除

11.使用hasOwnProperty验证对象属性不是来自原型链的
使用in操作符检查一个对象是否包含给定属性，不仅可以检查包含在引用对象中的属性，而且能够检查对象通过原型链继承的所有属性。

12.使用for in循环枚举对象属性
var cody = {
	age : 23,
	gender : 'male'
}
for (var key in cody){
	if(cody.hasOwnProperty(key)){
		console.log(key);
	}
}


13.Object()属性和方法
constructor
hasOwnProperty()
isPrototypeOf()
toLocaleStrinf()
toString()
valueOf()

14.使用对象字面量创建Object()对象，没有必要将属性指定为字符串，除非属性名是以下几种情况：保留关键字，包含空格或特殊字符，以数字开始


15.Function对象实例属性和方法
arguments 是一个类数组对象，包含所有传递给函数的参数
arguments.callee属性，它是对当前执行函数的引用，在函数需要递归调用，它非常有用
var foo = function foo(){
	console.log(arguments.callee);//输出foo()
}
constructor

length 实际上可以获取函数所需要参数总数量
*  var myFunction = function(z,s,d,e,r,m,q){
	return myFunction.length;
}
console.log(myFunction());//7

apply()

call()

toString()

16.在js中，函数是对象，意味着函数可以存储在一个变量，数组或对象中，函数可以传递给函数，并由函数返回，函数可以拥有属性，因为它是一个对象。








