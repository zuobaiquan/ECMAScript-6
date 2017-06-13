### 1.let和const命令

#### 1.1 let命令

代码块:	{} 包起来的代码， 形成了一个作用域，块级作用域，比如： if  for while

特点: 只能在代码块里面使用，而var 只有函数作用域

##### a). let具备块级作用域

##### b). 不允许重复声明

​          let a=12;

​          let a=5;	//错的

##### c).let不像var那样会发生”变量提升”现象

​	所以，变量一定要在声明后使用，否则报错

```javascript
console.log(foo);//Uncaught ReferenceError: foo is not defined
let foo=2;
```

上面的代码在foo之前就使用这个变量，结果会抛出一个错误。

> 这意味着typeof不再是一个百分之百安全的操作。
>
> typeof x;//Uncaught ReferenceError: x is not defined
>
> let x;

##### d)暂时性死区

只要块级作用域内存在`let`命令，它所声明的变量就“绑定”(binding)这个区域，不再受外部的影响。

```javascript
var tmp = 123;
if (true) {
	tmp = 'abc';//Uncaught ReferenceError: tmp is not defined
	let tmp;
}
```

上面代码中，存在全局变量`tmp`，但是块级作用域内`let`又声明了一个局部变量`tmp`，导致后者绑定这个块级作用域，所以在`let`声明变量前，对`tmp`赋值会报错。

> 总之，在代码块内，使用`let`命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```

总结: 其实let才接近其他语言的变量

总结: 块级作用域，其实就是 匿名函数立即调用

#### 1.2 为什么需要块级作用域

##### 1.2.1第一种场景

内层变量可能会覆盖外层变量









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

### 2.const——用来定义 常量

```
一旦赋值，以后再也修改不了了
```

```
const a=12;
a=15	//报错

注意:  const必须给初始值， 不能重复声明
	因为以后再也没法赋值了，所以声明的时候一定得有值

用途: 为了防止意外修改变量
	比如引入库名，组件名
```

## 