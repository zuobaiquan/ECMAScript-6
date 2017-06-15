### 1.let和const命令

#### 1.1 let命令

代码块:	{} 包起来的代码， 形成了一个作用域，块级作用域，比如： if  for while

特点: 只能在代码块里面使用，而var 只有函数作用域

##### a). let具备块级作用域

##### b). 不允许重复声明   

```javascript
let a=12;
let a=5;	//错的
```

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

##### e)块级作用域

外层代码块不受内层代码块的影响

```javascript
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
//上面的函数有两个代码块，都声明了变量n，运行后输出5。
//这表示外层代码块不受内层代码块的影响。
//如果使用var定义变量n，最后输出的值就是10。
```

总结: 其实let才接近其他语言的变量

总结: 块级作用域，其实就是 匿名函数立即调用

#### 1.2 为什么需要块级作用域

ES5 只有全局作用域和函数作用域，**没有块级作用域**，这带来很多不合理的场景。

##### 1.2.1第一种场景

内层变量可能会覆盖外层变量

```javascript
var tmp = new Date();
function f() {
  console.log(tmp);
  if (false) {
    var tmp = 'hello world';
  }
}
f(); // undefined
//说明：函数f执行，变量提升，导致内层的tmp变量覆盖了外层的tmp变量。
//更多关于变量提升看https://github.com/zuobaiquan/javascript/blob/master/js%E4%B8%AD%E7%9A%84%E5%8F%98%E9%87%8F%E6%8F%90%E5%8D%87.md
```

##### 1.2.2第二种场景

用来计数的循环变量泄露为全局变量

```javascript
var s = 'hello';
for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}
console.log(i); // 5
//上面代码中，变量i只用来控制循环，但是循环结束后，它并没有消失，泄露成了全局变量。
```









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

1. const声明一个只读的常量。一旦声明，常量的值就不能改变。

   ```javascript
   const a=12;
   a=15	//报错
   ```

2. const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。

   ```javascript
   const a;
   a=12;
   // Uncaught SyntaxError: Missing initializer in const declaration
   //对于const来说，只声明不赋值，就会报错。，而let可以先声明再赋值
   //const声明的常量，也与let一样不可重复声明。
   ```

3. `const`的作用域与`let`命令相同：只在声明所在的块级作用域内有效。

   ```javascript
   if (true) {
     const MAX = 5;
   }
   MAX // Uncaught ReferenceError: MAX is not defined
   ```

```
用途: 为了防止意外修改变量、比如引入库名，组件名
```

4. const本质

   > `const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指针，`const`只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。

```javascript
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```

上面代码中，常量`foo`储存的是一个地址，这个地址指向一个对象。不可变的只是这个地址，即不能把`foo`指向另一个地址，但对象本身是可变的，所以依然可以为其添加新属性。