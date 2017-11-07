
-  //document.getElementById("demo").innerHTML='change..'; /*单独改变一行  document指的是文档*/
- document.getElementById("demo").innerHTML="我的第一段 JavaScript";请使用 "id" 属性来标识 HTML 元素：id只能找到一个元素
- document.write("<p>我的第一段 JavaScript</p>");  请使用 document.write() 仅仅向文档输出写内容。
- 您可以在文本字符串中使用反斜杠对代码行进行换行
- JavaScript 语句和 JavaScript 变量都对大小写敏感
- 当您向变量分配文本值时，应该用双引号或单引号包围这个值。
- 我们使用 var 关键词来声明变量：值加引号是文本变量，不加引号是数值变量。
- var name="Gates", age=56, job="CEO"; 声明多个变量。
- JavaScript 函数

```
JavaScript 函数语法
函数就是包裹在花括号中的代码块，前面使用了关键词 function：
function functionname()
{
这里是要执行的代码
}

当您声明函数时，请把参数作为变量来声明：
function myFunction(var1,var2)
{
这里是要执行的代码
}

带有返回值的函数
function myFunction()
{
var x=5;
return x;
}

document.getElementById("demo").innerHTML=myFunction();

function myFunction(a,b)
{
if (a>b)
  {
  return;
  }
x=a+b
}

向未声明的 JavaScript 变量来分配值
如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明。
这条语句：
carname="Volvo";
将声明一个全局变量 carname，即使它在函数内执行。
```
- JavaScript的数据类型

```
JavaScript 拥有动态类型
var x                // x 为 undefined
var x = 6;           // x 为数字
var x = "Bill";      // x 为字符串

极大或极小的数字可以通过科学（指数）计数法来书写：
var y=123e5;      // 12300000
var z=123e-5;     // 0.00123

JavaScript 布尔
var x=true
var y=false

JavaScript 数组
var cars=new Array();
cars[0]="Audi";
cars[1]="BMW";
cars[2]="Volvo";
或者 (condensed array):
var cars=new Array("Audi","BMW","Volvo");

JavaScript 对象
对象由花括号分隔。在括号内部，对象的属性以名称和值对的形式 (name : value) 来定义。属性由逗号分隔：
var person={firstname:"Bill", lastname:"Gates", id:5566};
上面例子中的对象 (person) 有三个属性：firstname、lastname 以及 id。
空格和折行无关紧要。声明可横跨多行：
var person={
firstname : "Bill",
lastname  : "Gates",
id        :  5566
};
对象属性有两种寻址方式：
实例
name=person.lastname;
name=person["lastname"];

声明变量类型
当您声明新变量时，可以使用关键词 "new" 来声明其类型：
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;
```
- 引入方式

```
 <script src="js/hello.js"></script> <!--这是导入js的一种方法-->  head中引入
 
 <script>  内嵌入网页
 </script> 
```
# 练习题

1. 用 `JavaScript` 实现游戏 `tic-tac-toe`

  <img title="tic-tac-toe" src=".../image/javascript/tic_tac_toe.png" width="300"/>