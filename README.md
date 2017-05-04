# ECMAScript-6

ECMA是标准， js是实现

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
	
	在浏览器里面如何使用？
		需要用到编译工具
	
		babel	
		------------------------------------------
		traceur	——由Google出的编译器，把ES6语法编译为ES5
	
		bootstrap	引导程序，跟css里面认识bootstrap不一样

​    	let——用来定义变量

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


const——用来定义 常量
	一旦赋值，以后再也修改不了了

	const a=12;
	a=15	//报错

	注意:  const必须给初始值， 不能重复声明
		因为以后再也没法赋值了，所以声明的时候一定得有值

	用途: 为了防止意外修改变量
		比如引入库名，组件名

字符串连接:
	之前:
		var str='';
		var str=""

	反单引号:	var str= ``	字符串模板

	之前: 	'abc'+变量名+'ef'
	现在:	`abc${变量名}ef`









