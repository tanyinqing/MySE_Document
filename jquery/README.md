

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
- 向您的页面添加 jQuery 库   

```
<script type="text/javascript" src="jquery.js"></script>
``` 
- AJAX  异步请求提交
- cdn 分发网络 

# jQuery

<img src="../image/jquery/jQuery_logo.svg" title="jQuery" height="100">

> 教学要求

1. jQuery 基本使用

> 课外参考

1. [W3 School](http://www.w3schools.com/jquery/default.asp)