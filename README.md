# ECMAScript-6

## 1.ECMA是标准， js是实现

	1996	ES1.0	js稳定	Netscape将js提交给ECMA组织， ES正式出现
	1998	ES2.0	ES2.0正式发布
	1999	ES3.0	ES3被浏览器广泛支持
	2007	ES4.0	ES4过于激进，被废除了
	2008	ES3.1	4.0退化为严重缩水版的 3.1, 代号	Harmony（和谐）
	2009	ES5.0	ES5正式发布了，同时公布JavScript.next 也就后来 6.0
	2011	ES5.1	ES5.1 成为了ISO国际标准
	2013.3	ES6.0	ES6.0 制定草案
	2013.12 ES6.0	ES6.0 草案发布
	2015.6	ES6.0	ES6.0预计发布正式版， 同时Javascript.next指向 ES7.0

在浏览器里面如何使用？需要用到编译工具

	babel	
	------------------------------------------
	traceur	——由Google出的编译器，把ES6语法编译为ES5
	
	bootstrap	引导程序，跟css里面认识bootstrap不一样

## 2.let——用来定义变量

代码块:	{} 包起来的代码， 形成了一个作用域，块级作用域，比如： if  for while

特点: 只能在代码块里面使用，而var 只有函数作用域

​    a). let具备块级作用域

​    b). 不允许重复声明

​          let a=12;

​          let a=5;	//错的

总结: 其实let才接近其他语言的变量

总结: 块级作用域，其实就是 匿名函数立即调用

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
//    window.onload=function(){
//        var btn=document.getElementsByTagName("input");
//        for(var i=0;i<btn.length;i++){
//            btn[i].onclick=function(){
//                alert(i);
//            }
//        }
//    }
    //发现弹出都是3
    //变量i是var声明的，在全局范围内都有效，所以全局只有一个变量i
    //每一次循环，变量i的值都会发生改变，而循环内被赋给数组a的function在运行时
    //会通过闭包读到这同一个变量i，导致最后输出的是最后一轮的i的值，也就是10
    //改进：封闭空间
//    window.onload=function(){
//        var btn=document.getElementsByTagName("input");
//        for(var i=0;i<btn.length;i++){
//            (function(i){
//                btn[i].onclick=function(){
//                    alert(i);
//                }
//            })(i)
//        }
//    }
      //改进，利用es新特性 let，，即把var变量换成 let即可
      window.onload=function(){
        var btn=document.getElementsByTagName("input");
        for(let i=0;i<btn.length;i++){
            btn[i].onclick=function(){
                alert(i);
            }
        }
      }
    </script>
</head>
<body>
<input type="button" value="按钮1">
<input type="button" value="按钮2">
<input type="button" value="按钮3">
</body>
```

## 3.const——用来定义 常量

	一旦赋值，以后再也修改不了了

	const a=12;
	a=15	//报错
	
	注意:  const必须给初始值， 不能重复声明
		因为以后再也没法赋值了，所以声明的时候一定得有值
	
	用途: 为了防止意外修改变量
		比如引入库名，组件名

## 4.字符串连接

	之前:
		var str='';
		var str=""
	
	反单引号:	var str= ``	字符串模板
	
	之前: 	'abc'+变量名+'ef'
	现在:	`abc${变量名}ef`

## 5.复制数组

```javascript
var arr=[1,2,3];
//引用赋值
var arr2=arr;
arr2.pop();
console.log(arr,arr2);
//此时arr和arr2都是 Array(2) 0: 1  1: 2  length: 2
```

#### a). 循环

```javascript
var arr=[1,2,3];
//循环
var arr2=[];
for(var i=0;i<arr.length;i++){
  arr2[i]=arr[i];
}
arr2.pop();
console.log(arr,arr2);
//此时arr是 Array(3) 0: 1  1: 2 2:3 length: 3
//此时arr2是 Array(2) 0: 1  1: 2 length: 2
```

#### b). Array.from(arr)

```javascript
var arr=[1,2,3];
//Array.from(arr)
var arr2=Array.from(arr);
arr2.pop();
console.log(arr,arr2);
//此时arr是 Array(3) 0: 1  1: 2 2:3 length: 3
//此时arr2是 Array(2) 0: 1  1: 2 length: 2
```

#### c). var arr2=[...arr];

使用 rest 参数（形式为“...变量名”），用于获取函数的多余参数

```javascript
var arr=[1,2,3];
//var arr2=[...arr];
var arr2=[...arr];
arr2.pop();
console.log(arr,arr2);
//此时arr是 Array(3) 0: 1  1: 2 2:3 length: 3
//此时arr2是 Array(2) 0: 1  1: 2 length: 2

//arguments对象并不是一个数组，但是访问单个参数的方式与访问数组元素的方式相同
function show(){
  console.log(arguments); 
  //arguments.push(5);   //此时报错arguments.push is not a function
}
show(1,2,3,4);

//改进：
function show(...arr){
	arr.push(5);
	console.log(arr);
}
show(1,2,3,4);
```

## 6.Map对象

和json相似，也是一种key-value形式，Map对象为了和for of循环配合而生的


```javascript
let mymap=new Map();
//设置:map.set(name,value);
mymap.set('a','apple');
mymap.set('b','banana');
//以上代码改写，一次性声明和赋值
// let mymap = new Map([
//   ['a','apple'],
//   ['b','banana'],
// ]);
console.log(mymap);//Map(2) {"a" => "apple", "b" => "banana"}
//alert(mymap.a);//undefined  不能这样访问
//获取：map.get(name)
console.log(mymap.get("a"));//apple
//删除：map.delete(name)
mymap.delete("a");
console.log(mymap);//Map(1) {"b" => "banana"}
mymap.set('a','apple');
for(var name of mymap){
  console.log(name); // b,banana   a,apple
}
//获取 key 和 value
for(var [key,value] of mymap){
  console.log(key, value); // key value
}
for(var [key] of mymap){
  console.log(key); // key
}
//默认调用entries    mymap默认就是map.entries()
for(var [key,value] of mymap.entries()){
  console.log(name);
}
//只是循环key
for(var key of mymap.keys()){ 
  console.log(key);
}
//只是循环value
for(var val of mymap.values()){     
  console.log(val);
}

var arrData=['红楼梦','三国演义','水浒传','西游记','金瓶梅'];
//for.. of也可以循环数组
//只循环值: for(var value of arr){}
for(var name of arrData){
  console.log(name);
}
//只循环索引:for(var key of arr.keys()){}
for(var name of arrData.keys()){
  console.log(name);
}
//索引和值都循环： for(var some of arr.entries()){}
for(var name of arrData.entries()){
  console.log(name);
}
```
注意：遍历map， 不能使用for in，没有效果

## 7.函数

#### es6之前

```javascript
function show(){
  alert(1);
}
show();
function show(a){
  return a;
}
show(12);
function show(a,b){
  return a+b;
}
show(12,5);
```
#### 箭头函数

```javascript
//var show=a=>a;      function show(a){return a};
//var f = () => 5;      // 等同于 var f = function () { return 5 };
var show=a=>a;
console.log(show(5));// 5

//var show=(a,b)=>a+b;      function show(a,b){return a+b};
var show=(a,b)=>a+b;
console.log(show(5,4));// 9

var a=101;
var testJson={
  a:1,
  b:2,
  show:()=>{
    //使用箭头函数 this问题， this指向了window
    console.log(this.a);//输出 101
    console.log(this.b);//输出 undefined
  },
  //注意这里的区别，下面没有使用箭头函数的写法
  show2(){
    console.log(this.a);//输出 1
    console.log(this.b);//输出 2
  }
};
testJson.show();
testJson.show2();
function testShow1(){
  console.log(arguments);
}
testShow1(1,2,3);//(3) [1, 2, 3, callee: function, Symbol(Symbol.iterator): function]
var testShow2=()=>{
  //arguments， 不能使用了
  //console.log(arguments);
};
testShow2(1,2,3);//Uncaught ReferenceError: arguments is not defined
```

## 8.对象

### 对象语法简洁化

```javascript
var birth = '2000/01/01';
var Person = {
  name: '张三',
  //等同于birth: birth
  birth,
  // 等同于hello: function ()...
  hello() { console.log('我的名字是', this.name); }
};
console.log(Person);//Object birth:"2000/01/01" hello:function hello() name:"张三"
```

### 面向对象

#### es6之前

```javascript
//es6之前的写法，不是真正的面向对象
//人类  工人类
function Person(name,age){  //既是类又是构造函数
  	this.name=name;
  	this.age=age;
}
Person.prototype.showName=function(){
	return this.name;
};
Person.prototype.showAge=function(){
	return this.age;
};

var p1=new Person('abc',10); 
console.log(p1); //Person {name: "abc", age: 10} __proto__:Object showName Object showAge
console.log(p1.showName());//abc
```

#### es6

类	class

构造函数	constructor	生成完实例以后，自己就执行的

```javascript
//es6之前的写法，不是真正的面向对象
//ES6之前的版本中没有类和实例，是通过原型prototype完成面向对象编程。
//人类  工人类
function Person(name,age){  //既是类又是构造函数
  this.name=name;
  this.age=age;
}
Person.prototype.showName=function(){
  return this.name;
};
Person.prototype.showAge=function(){
  return this.age;
};

var p1=new Person('abc',10); 
console.log(p1); //Person {name: "abc", age: 10} __proto__:Object showAge Object showName
console.log(p1.showName());//abc

//es6
//类 class，类名首字母大写
class People{ 
  //构造函数  
  ////constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。
  //一个类必须有constructor方法，如果没有显式定义，
  //一个空的constructor方法会被默认添加。constructor() {}
  //构造器中也可以不给默认值constructor(name,age){
  constructor(name='default',age=0){
    this.name=name;
    this.age=age;
  }
  showName(){
    return this.name;
  }
  showAge(){
    return this.age;
  }
}
var p2=new People('abc',10); 
console.log(p2); 
//Person {name: "abc", age: 10} __proto__:constructor:class People Object showAge Object showName
//相比原来多了constructor
console.log(p2.showName());//abc
var p3=new People('bbb',20);
console.log(typeof p2.showName);//function
console.log(p2.showName==p3.showName);//true
console.log(p2.showName()==p3.showName());//false
console.log(p2.constructor==People);//true

var p3=new People(); 
console.log(p3.showName());//default
//继承   es6之前:  子类.prototype=new 父类();
//es6
//继承
class Worker extends Person{
  constructor(name,age,job='扫地的'){
    super(name,age);////直接调用父类构造器进行初始化
    //super()只能用在子类的构造函数之中，用在其他地方就会报错。
    this.job=job;
  }
  showJob(){
    return this.job;
  }
  showName(){
    return "起点"+this.name+"终点";
  }
}
var w1=new Worker('mmm',56);
console.log(w1.showJob());//扫地的
console.log(w1.showName());//起点mmm终点
```

```javascript
//static 关键字用来定义类的静态方法。
//静态方法是指那些不需要对类进行实例化， 使用类名就可以直接访问的方法
//需要注意：静态方法不能被实例化的对象调用。
//静态方法经常用来作为工具函数。
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;
    return Math.sqrt(dx*dx + dy*dy);
  }
}
const p1 = new Point(1, 1);
const p2 = new Point(2, 2);
console.log(Point.distance(p1, p2)); //根号2 即1.4142135623730951
```

## 9.模块

## 10Promise对象

异步: 多个操作可以同时进行


	//ajax
	ajax(url,function(){
		//1
	},fnFail);
	//2
Promise就是一个对象，用来传递异步操作的数据(消息)

	pending（等待、处理中）
			—> Resolve(完成、fullFilled)
			—> Rejected(拒绝、失败)
使用：
```javascript
var p1=new Promise(function(resolve,reject){
	//resolve  成功了
	//reject    失败了
    	});

var p1=new Promise(function(resolve,reject){
	if(异步处理成功了){
		resolve(成功数据)
	}else{
		reject(失败原因)
	}
    	});

p1.then(成功(resolve),失败(reject))	√
--------------------------------------------

p1.catch——用来捕获错误

--------------------------------------------
Promise.all——全部，用于将多个promise对象，组合，包装成一个全新的promise实例
	Promise.all([p1,p2,p3...]);

	所有的promise对象，都正确，才走成功
	否则，只要有一个错误，是失败了
--------------------------------------------
Promise.race——返回也是一个promise对象
	最先能执行的promise结果， 哪个最快，用哪个
--------------------------------------------
Promise.reject()	——生成错误的一个promise

--------------------------------------------
Promise.resolve()	——生成一个成功的promise对象
	语法：
		Promise.resolve(value)
		Promise.resolve(promise)
```
简单的实例

```javascript
var p1=new Promise(function(resolve,reject){
  	resolve(1);
});
p1.then(function(value){
  	//此时执行这一条
  	alert('成功了:'+value);
},function(){
  	//如果是reject，则执行这一条
  	alert('失败了');
});
```