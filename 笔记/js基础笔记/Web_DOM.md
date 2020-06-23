## DOM
- 页面，用document表示   标签为元素，用element表示  页面中所有内容(标签、属性、文本、注释等)都是节点，node -----DOM把以上内容看做对象。
### 操作元素
    - getElementById根据id获取元素对象    getElementsByTagName 返回元素对象集合   
      Element.getElementsByTagName 获取某元素中的某类标签   .body .documentElement
    - getElementsByClassName按类名取元素对象集合（H5）

    - querySelector('选择器'H5) 方法返回文档中匹配指定 CSS 选择器的一个元素。
      指定一个或多个匹配元素的 CSS 选择器。 可以使用它们的 id, 类, 类型, 属性, 属性值等来选取元素。querySelectorAll

对于多个选择器，使用逗号隔开，返回一个匹配的元素。
        console.dir打印返回的元素对象，查看里面的属性和方法

    - 事件：事件源 事件类型  事件处理程序
            获取事件源，注册事件(绑定事件)，添加事件处理程序(函数赋值形式)
    - 鼠标事件：
        onmouseover(out)  onfous获得焦点 onblur失去焦点  onmousemove移动 onmouseup弹起 --down按下

    - 操作元素
        （操作普通盒子）改变元素内容、获取元素：element.innerText(HTMl)    HTML保留标签 格式  打印全部内容

    - 操作表单
            disable禁用  type(password、text等等)属性
    - 样式
            行内样式操作：element.style.width（backgroundColor） 行内样式权重高
            类名样式操作：element.className  给元素添加类名的方式修改样式
                把修改后的样式写在css里的属性为.change{}中，js事件中给对象填加进这个类this.className='change'。
                保留原来类名，把原来类名写进className中，即为多类名选择器

    - 排他思想 ：有同一组元素，想要某一元素实现某种样式，用循环的排他思想
                1、所有元素清除样式
                2、给当前设置样式
    
    - 多个相同的元素用循环绑定事件
属性值都是字符串格式  变量需要拼接字符串

    - 复选框案例
            下面复选框全部选中，上面的全选才能选中。
            1、给下面复选框循环绑定单击事件
            2、每次点击下面复选框循环检查是否全部被选中
            3、全部选中就给全选框checked属性为true
#### 案例 全选框
```js
//t表示下面复选框，t_all表示全选框
for (var i = 0; i < t.length; i++) {
    t[i].onlick = function{
        var flag = true; //flag控制全选框是否选中
            for (var i = 0; i < t.length; i++) {
            if (!t[i].checked) {
                flag = false;
            }
        }
        t_all.checked = flag;
    }
```
    - 自定义属性操作
        1、element.属性  element.getAttribute('属性');获取属性值
            获取自带内置属性      主要获得自定义属性
            element.setAttribute('属性','值')  removeAttribute移除属性
#### 案例 tab栏切换 
    1、下面内容会随着Tab栏切换改变  让下面和上面一一对应
    2、给上面list中li添加自定义属性，从0开始
    3、当点击li时，让下面对应序号的内容显示（内容按顺序排列），其余隐藏。排他思想

    - H5设置自定义属性
        data-开头  H5新增----element.dataset.index获取    dataset获取data自定义属性集合

### 节点
    1、利用节点层级关系获取元素  nodeType节点类型  nodeName节点名称  nodeValue节点值
        元素节点nodetype为1  属性节点2   文本（文字、空格、换行等）3
    2、利用DOM树把节点分为不同层级，父子兄层级
            - 父子节点 例子：var zi = document.querySelector('子元素');
                      zi.parentNode拿到父元素
                      childNodes所有子节点元素，包含元素节点、文本节点。一般不是用
            - children获取所有子元素节点--实际开发常用的  children[0]第一个子元素         
            - 兄弟节点
                     nextSibling  nextElementSibiling   previous
    3、创建节点
            - createElement('tagName')元素原来不存在，根据需求动态创建，动态创建节点      
            - node.appendChild(child)间节点添加到指定父节点的子节点列表末尾。类似css伪元素after
                     node.insertBefore(child,指定元素)将元素添加到指定元素之前
    4、删除节点
            - node.removeChild(子节点元素);删除节点中子元素
    5、克隆节点
            -node.cloneNode(true) 为空或false，浅拷贝，只复制标签不复制内容   
#### 案例-发布评论 删除评论
```js
 // 发布评论的案例
 // textarea 定义多行的文本输入控件。文本区中可容纳无限数量的文本
        //获取元素，发布按钮、文本框、评论列表
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        //注册事件
        btn.onclick=function(){
            if(text.value==''){
                alert('你没有输入内容');
            }else{
                //创建元素
                var li = document.createElement('li');
                //把文本框文字给li
                li.innerHTML=text.value + "<a href='javascript:;'>删除</a>";
                //把li添加到ul评论列表中,添加到最前面
                ul.insertBefore(li,ul.children[0]);
                //删除元素  删除掉的是当前a链接的li标签
                var as = document.querySelectorAll('a');
                for (var i = 0; i < as.length; i++) {
                    as.onclink = function(){
                        //删除评论列表ul中的li评论  当前a所在的li a的父亲
                        ul.removeChild(this.parentNode);
                    }
                }
            }
        }
```
### 创建元素
    - innerHTML='字符串';拼接字符串   创建多个元素，采用数组形式拼接效率高

        var arr = [];
         for (var i = 0; i <100 ; i++) {
             arr.push('a标签');      
        }
        div.innerHTML = arr.join('');//没有分隔符。默认逗号

    - createElement('元素'); 效率稍低，结构清晰
### DOM核心
    - Document Object Model  文档对象模型
    1、创建  innerHTML createElement
    2、appendChild  insertBefore
    3、removeChild
    4、-修改元素属性  -修改普通元素内容  
       -修改表单元素(value,type,disable)  -修改元素样式(style,className)
    5、querySelector  parentNode   children
    6、getAttribute自定义属性    set   remove
### 事件
    - 监听注册方式  addEventListener  H5
        同一事件，同一元素添加多个监听器（事件处理程序）
        document.getElementById("myBtn").addEventListener("click", function(){
              document.getElementById("demo").innerHTML = "Hello World";
         });
    - 删除事件
        1、element.onclick = 'null';
        2、element.addEventListener('click',fn)；// 如果要移除事件句柄，addEventListener() 的执行函数必须使用外部函数
           function fn(){
               element.removeEventtListener('click',fn);
           }
### DOM事件流
    -1，事件捕获阶段。2，处于目标阶段3，事件冒泡阶段。
    -js只能执行捕获或冒泡其中一个阶段
    -oncilc和attachEvent（ie）得到冒泡阶段
    -addEventListener第三个参数为true，捕获阶段 document->html->body->father->son

    -冒泡阶段 参数为false  顺序相反（重要，捕获很少用）
### 事件对象
    - 写在监听函数小括号里面，当形参来看。 event e
    - 是一系列相关数据的集合，比如鼠标点击包含了鼠标的相关信息
    - 兼容性处理   e = e || window.event;

    - 常见属性
        -e.target触发事件对象  type preventDefault

    - 阻止行为，让连接不跳转  e.preventDefault()
    - 阻止冒泡：e.stopPropagation
    - 事件委托：不是每个子节点单独设置事件监听器，而是事件监听器设置在父节点上，利用冒泡原理影响设置每个子节点
    e.target触发事件对象
    - 鼠标事件
        ontextmenu 可以用e.preventDefault()禁用右键菜单
        selectstart  可以用e.preventDefault()禁止选中
    - 鼠标事件对象
        clientX Y  可视区的坐标    pageX Y 文档页面坐标    screenX电脑屏幕坐标

#### mousemove图片跟随案例
```
var picture = document.querySelector('img');
document.addEventListrner('mousemove', function(e){
    picture.style.left = e.pageX //图片坐标跟随鼠标坐标
    picture.style.top = e.pageY
})
```
### 常用键盘事件
    - onkeyup松开触发   onkeydown按下触发    keypress不识别功能键
    顺序down-press-up
    - 键盘事件对象
        keyCode获取响应键的ASCII码  
        up dowm不区分大小写