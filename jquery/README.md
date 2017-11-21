
### 项目清单列表
|名称|说明|地址|
|---|---|---|
|jQuery_20170902|这个是项目的地址|[地址](https://github.com/tanyinqing/jQuery_20170902)|
|1_Hello|jQuerty选择器选择元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/1_Hello.html)|
|2_selector|jQuerty选择器选择类元素的并集|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/2_selector.html)|
|3_even-old|jQuerty选择器选择第几个元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/3_even-old.html)|
|4_attribute|jQuerty选择器选择具有特定属性值的元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/4_attribute.html)|
|5_input|jQuerty选择器选择表单中的某个元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/5_input.html)|



- 文档就绪函数 保证文档全部加载后执行函数
```
<script>
        $(function () {  就绪函数
            $('p').click(function () {
                $(this).hide();
            })
        })
    </script>
代码从上向下执行
```

- jQuery 语法
    - jQuery 语法是为 HTML 元素的选取编制的，可以对元素执行某些操作。
    - 基础语法是：$(selector).action()
    - 美元符号定义 jQuery
    - 选择符（selector）“查询”和“查找” HTML 元素
    - jQuery 的 action() 执行对元素的操作
- https://jquery.com/ 下载js的地址
    - production jQuery 3.2.1 表示是压缩版
    - development jQuery 3.2.1  表示是开发版
- 向您的页面添加 jQuery 库   

```
<script type="text/javascript" src="jquery.js"></script>
``` 
- AJAX  异步请求提交
- cdn 内容分发网络 

# jQuery

<img src="../image/jquery/jQuery_logo.svg" title="jQuery" height="100">

> 教学要求

1. jQuery 基本使用

> 课外参考

1. [W3 School](http://www.w3schools.com/jquery/default.asp)