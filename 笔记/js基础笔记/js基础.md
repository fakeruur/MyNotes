## 基础

    prompt输入框  alert弹出 console.log控制台输出 
    var a；声明变量  同时声明变量一个var，用逗号隔开

    命名规范：
        区分大小写，不以数字开头，有意义，驼峰命名，不能关键字，可用_ $
    
    数据类型：
        弱类型语言，动态语言，根据右边变量值来确定类型

        数字前0八进制，0x十六进制 infinity NaN非数字

        isNaN判断非数字  js推荐单引号表示字符串嵌套用不同

        转义符：\ \n换行 \t缩进 \b空格

        str.length获取字符串长度   

        字符串拼接：只要字符串和其他拼接，一定是字符串类型
            引引加加   “李“+age+”辉”

        typeof 获取类型


    类型转换：表单获取来的为字符串。有时要转换为数字
        转换字符串：toString  String()强转   拼接加空字符串：num+''
        转换数字型：parselent(String)取整、去掉px单位  parseFloat(String)浮点数 Number()  js隐式转换(- * /)算术运算自动转换‘12’-0
        Boolean（0、‘’、NaN、null、undef）false 
        
## 运算符

    不要判断两个浮点数是否相等
    ===全等、要求值和数据类型都一致  ==等号、会转型
    &&  ||  !  
    逻辑中断（逻辑与短路运算：表达式1真，返回表达式2.1假，返回1.）
            （逻辑或：和上面相反，1真反1）
    一元运算符里逻辑非优先级很高  与比非高

## 流程控制

    三元运算符  条件表达式 ？ 表达式1 ： 表达式2
    switch(表达式){   switch..case处理case比较确定值的情况    if判断范围
        case value1：
           执行语句；       断点调试 f12 source
           break；
        default：
           最后语句；
        }

    while   do{循环体}while(条件表达式)先执行，再判断   

## 99乘法表

```js
var str = '';
for(var i = 1; i <= 9; i++){
    for(var j = 1; j <= i; j++){
        str += j + '×' + i + '=' + i * j + '\t';
    }
    str += '\n';
}
 console.log(str);     
```

## 数组

    var arr = new Array();创建一个空数组  var arr = [];空数组
    遍历数组 求最大值：第一个值给max，遍历比较与max的大小，比max大，把值给max。

    arr.length = 5;直接修改数组长度  不要给数组名赋值，会覆盖掉数组数据
    反转数组：(var i = arr.lenth - 1, i>=0,i--); 最后一个值   newArray[newArray.length] = arr[i];

### 冒泡排序：
```js
        for (var i = 0; i < arr.length - 1; i++) {
            for (var j = 0; j < arr.length - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    var temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp
                }
            }
        }
```

## 函数

    1、形参看做不用声明的变量  return接收一个值
    2、内置函数 arguments(伪数组)存储所有传递来的实参
    3、function(){}命名函数  var fun = function(){}匿名函数

## 作用域

    全局变量：全局作用域下的变量  
        浏览器关闭才会销毁
        在函数内部，没有声明直接赋值的变量也属于全局变量
    局部变量 函数内部
    块级作用域....ES6

    作用域链：内部函数访问外部函数的变量，采取链式查找的方法来决定取哪个字值
    就近原则，谁离得近取谁

## 预解析

    js解析器运行js代码：预解析和代码执行 
        1、js引擎会js里面所有的var和function提升到作用域最前面
            -变量提升和函数提升
                变量：变量声明提升到作用域最前面。不提升赋值操作
                函数：函数声明提升到作用域最前面。不调用函数
        2、代码从上到小执行

```js
//作用域例题...提升变量声明和函数声明，其他不变，代码顺序执行
var num = 10;
fun();
function fun(){
    console.log(num);
    var num = 20;
}  //输出值：undefined
```
var a=b=c=1；相当于 var a = 1；b = 1；c = 1；
集体声明：var a = 1，b = 1，c = 1；

## js对象

    创建对象：
        1、var obj = {name:'李辉'， age:18,对象的属性 sayHi: function(){方法体}这个叫对象的方法 }；
            调用： obj.name;  obj['name'];  obj.sayHi();
        2、var obj = new Object();  obj.name='刘宏';添加属性   obj.sayHi=function(){};

        3、构造函数
            function Star(name, age, sex){        调用：var ligou = new Start('李狗', 18, '男');
                this.name=name;                         ligou.sing('冰雨');              
                this.age=age;
                this.sing=function(song){
                    console.log(song);
                }
            }  名字首字母大写

    遍历对象:
            for (const key in object) {
                if (object.hasOwnProperty(key)) {
                    const element = object[key];
                }
            }

## 内置对象

    自带对象，一些常用的功能(属性和方法)

```js
//封装数学对象
var myMax = {
    PI:3.14,
    max: function(){
        var max = arguments[0];
        for(vari=1;i<arguments.length;i++>){
            if(arguments[i]>max){
                max=arguments[i];
                }
        }
        return max;
    }
}
```

    math: floor向下取整  ceil向上 round四舍五入   random随机数
    Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
    Date是一个构造函数 要实例化  var date = new Date();

    获取当前秒数（时间戳）  getTime  valueOf    var date = +new Date();  Date.now()h5新增

#### 倒计时

![avatar](./img/倒计时.png)

    数组：
        instanceof 运算符  检测是否为数组
        Array.isArray(参数);  检测数组  H5
    增删：push在后面追加，返回结果是新数组长度
         unshift在前面加
         pop删除最后参数，返回值为删除的元素
         shift删除前面
    reverse反转   sort冒泡排序

#### sort冒泡排序

```js
arr.sort(functionn(a,b){
    return a - b //升序排列，b-a降序
})
```
    indexOf(元素，起始位置) 获取索引  找不到返回-1   lastIndexOf
#### 数组去重：遍历旧数组去查询新数组，新数组没有就把它放进去
```js
function unique(arr){
    var newArry = [];
    for (var i = 0; i < arr.length - 1; i++) {
         if(newArry.indexOf(arr[i] === -1)){
             newArr.push(arr[i];)
         }
    }
    return newArry;
}
```
    toString  join('分隔符')转换字符串，中间加符号，默认逗号

    字符串对象：
        基本包装类型就是把简单数据类型包装成复杂数据类型，这样基本类型就有了属性和方法
        字符串不可变，修改只是心创建了一个，原来的还在内存中

    根据位置返回字符：
        charAt(index)根据位置返回字符   charCodeArt返回索引号的ASCII值，判断用户按了哪个键  str(index)H5
    
    字符串操作方法：
            截取字符串，substr(索引号，取几个值)
            替换字符。replace  全部替换用循环，
            split(字符串所用分隔符)  字符串转换为数组

## 简单数据类型和复杂数据类型

    简单又叫基本类型、值类型     复杂叫引用类型：用new创造的
    null-----空对象
    简单类型传参是复制了一份值给形参，复杂数据类型是复制了地址给形参