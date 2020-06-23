## jQuery
    - 基本使用
        等着页面DOM加载完毕再去执行js代码 $就是JQuery的顶级对象，把元素包装成jQuery对象，调用jQuery的方法
        $(function() {
            $('div').hide();
        })
    - jQuery对象：对DOM包装后产生的对象（伪数组形式） $('div')只能使用jQuery方法  原生对象用原生方法
    - 相互转换：$('div')[0]转换为DOM对象
### jQuery选择器
- $('') css选择器一样  
- $('div').css("background","pink") 隐式迭代把匹配的所有元素内部进行遍历，执行相应的方法
- $("li:eq(2)")选索引号为2的li'    odd奇数   oven偶数
- jQuery筛选方法   $("li").parent()  find后代  sibilings兄弟节点不包含自身   nextAll prevAll同辈元素  hasClass检查含有某个特定元素返回true     eq(0)按index
- 排他思想
```js
$(function(){
    $("button").click(function(){
        $(this).css("background","pink"); //当前变化
        $(this).siblings("button").css("background","")； //其他去掉
    })
})
```
### jQuery样式操作
- 修改样式$(this).css("background","pink")
```js
$(this).css({  //参数以对象形式
    width:400,
    height:200，
    backgroundColor："pink"
})
```
- $("div").addClass("current")添加类  removeClass  toggleClass切换类
### jQuery效果
- 显示隐藏
    - show([speed], [easing], [fn])
    - hide toggle
    - slideUp  slideDown slideToggle里面的值一样
    - 事件切换hover(function(){},function(){})鼠标经过和离开
```js
$("div").hover(function(){  //下拉菜单
    $(this).children("div").stop().slideToggle();  //stop结束上一次的动画
})
```
    - 动画或效果队列
        效果一触发就会执行，多次触发就会造成效果排队执行
- 淡入淡出
    - fadeIn fadeOut fadeToggle([speed], [easing], [fn])
    - fadeTo([speed], opacity,[easing], [fn])透明度必须写0-1
- 自定义动画animate
    - animate(params,[speed], [easing], [fn]) params:想要更改的样式
        - animate({left:500,top:300,width:500},500)//
#### 手风琴 折叠卡片
```js
$(function() {
    // 鼠标经过某个小li 有两步操作：
    $(".king li").mouseenter(function() {
        // 1.当前小li 宽度变为 224px， 同时里面的小图片淡出，大图片淡入
        $(this).stop().animate({
            width: 224
        }).find(".small").stop().fadeOut().siblings(".big").stop().fadeIn();
        // 2.其余兄弟小li宽度变为69px， 小图片淡入， 大图片淡出
        $(this).siblings("li").stop().animate({
            width: 69
        }).find(".small").stop().fadeIn().siblings(".big").stop().fadeOut();
    })
})
```
### 属性操作
- element.prop("属性","内容") 获取  设置、固有属性
- attr()自定义属性
- 事件change状态变化就可执行
- :checked选择器  查找被选中的表单元素
- addClass
#### 案例：购物车全选
### 内容文本值
- html()获取元素、设置元素内容
- text获取文本内容
- val表单内容
    - 案例：购物车
- parents所有的父级元素
- toFixed保留几位小数
### 元素操作
- 遍历元素
    - each(ffunction(index,domEle){}) domEle是个DOM对象不是jquery对象
```js
        $(function() {
            var sum = 0;
            // 1. each() 方法遍历元素 
            var arr = ["red", "green", "blue"];
            $("div").each(function(i, domEle) {
                // 回调函数第一个参数一定是索引号  可以自己指定索引号号名称
                // 回调函数第二个参数一定是 dom元素对象 也是自己命名
                $(domEle).css("color", arr[i]);
                sum += parseInt($(domEle).text());
            })
            console.log(sum);
            // 2. $.each() 方法遍历元素 主要用于遍历数据，处理数据
            $.each($("div"), function(i, ele) {
                });
            $.each(arr, function(i, ele) {
                })
            $.each({
                name: "andy",
                age: 18
            }, function(i, ele) {
                console.log(i); // 输出的是 name age 属性名
                console.log(ele); // 输出的是 andy  18 属性值
            })
        })
```
- 创建元素
    - $("<li></li>")
- 添加
    - 内部添加 append prepend
    - 外部添加 after before
- 删除
    - remove 删除匹配元素
    - empty 删除子节点
## jquery事件
### 事件
- 事件处理on()绑定事件
    - element.on(events,[selector],fn) 
        - 多个events用逗号隔开
        - selector 元素的子元素选择器
```js
$("div").on({ //多事件处理
     mouseenter:function(){
        $(this).css("color","pink");
     },
     click:function(){
        $(this).css("background","blue");
     }
})
$("div").on("mouseenter mouseleave",function{
    $(this).toggleClass("current");
})
```
- 实践委派
    - $("ul").on("cilick","li",function(){})----把原来加给子元素的事件绑定在父元素身上，把事件委派给父元素
- off解绑事件