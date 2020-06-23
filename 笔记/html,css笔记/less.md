## less
    一门css的预处理语言，对css增强，通过less可以编写更少的代码实现更强大的样式
#### less常用语法
    选择器父子兄弟关系可以嵌套编写，然后解析为css样式。
```lcss
//   变量 @变量名：变量值；
@a:200px;
@c:box1;//代替类名

.box2{
    color：red；
    background-color：$color;// 直接使用属性名引用其值
    width:@a;
}
.@{c}{ //作为类名使用
    width:@a;
}

@images:"../img";//路径名
body{
    background:url("@{images}/1.png");
}

也可以代替属性名  @property:color;   用 @{property}：red；

.box1{
    &:hover{ //&表示外层父元素
        color:red;
    }
}

.box1{
    color:red;
}
.box2:extend(.box1){ //对当前选择器扩展指定选择器的样式
    width:1px;
}
.box3{
    .box2(); //混合，对box2的样式进行复制
}

.box(){  //创建一个mixin 类似接口
    color:red;
    width:1px;
    height：2px；
}
.box4{
    .box; //调用样式，相当于复制
}

.box(@a,@b){  //混合函数、、也可以设定默认值，直接调用或者重新赋值
    color:@a;
    width:@b;
    height：2px；
}
.box5{
    .box(100px,200px); //传参
}
```
#### less补充

```
//lessd的数值可以直接进行运算
@import "1.less";//可以引入其他less
```
