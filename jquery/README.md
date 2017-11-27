
### day1  教程的地址  http://w3school.com.cn/jquery/
|名称|说明|地址|
|---|---|---|
|jQuery_20170902|这个是项目的地址|[地址](https://github.com/tanyinqing/jQuery_20170902)|
|1_Hello|jQuerty选择器选择元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/1_Hello.html)|
|2_selector|jQuerty选择器选择类元素的并集|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/2_selector.html)|
|3_even-old|jQuerty选择器选择第几个元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/3_even-old.html)|
|4_attribute|jQuerty选择器选择具有特定属性值的元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/4_attribute.html)|
|5_input|jQuerty选择器选择表单中的某个元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day1/5_input.html)|

### day2  教程的地址  http://w3school.com.cn/jquery/
|名称|说明|地址|
|---|---|---|
|1_show-hide|jQuery效果隐藏和显示|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/1_show-hide.html)|
|2_fade|jQuery效果淡入淡出|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/2_fade.html)|
|3_slide|jQuery 滑动方法可使元素上下滑动。|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/3_slide.html)|
|4_animate|jQuery animate() 方法允许您创建自定义的动画|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/4_animate.html)|
|5_html-text-val|jQuery 拥有可操作 HTML 元素和属性的强大方法|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/5_html-text-val.html)|
|6_attr|jQuery attr() 方法也用于设置/改变属性值|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/6_attr.html)|
|7_create|通过 jQuery，可以很容易地添加新元素/内容。|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/7_create.html)|
|8_remove-empty|通过 jQuery，可以很容易地删除已有的 HTML 元素|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day2/8_remove-empty.html)|

### day2  教程的地址  http://w3school.com.cn/jquery/
|名称|说明|地址|
|---|---|---|
|1_css|jQuery - 获取并设置 CSS 类|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day3/1_css.html)|
|2_width_height|通过 jQuery，很容易处理元素和浏览器窗口的尺寸|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day3/2_width_height.html)|
|3_traversing|jQuery 遍历 - 祖先  和后代|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day3/3_traversing.html)|
|4_siblings|jQuery 遍历 - 同胞|[地址](https://github.com/tanyinqing/jQuery_20170902/blob/master/day3/4_siblings.html)|

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