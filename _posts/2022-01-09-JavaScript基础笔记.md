---
layout: mypost
title: JavaScript基础笔记
categories: [JavaScript]
---

*#音量注意：没有调节音量的功能，播放前请注意设备音量*

<iframe src="//music.163.com/outchain/player?type=2&id=1373604201&auto=0&height=66" frameborder="0" width="100%" height="86px" ></iframe>

## 序

> 1. 记录的内容可能不全，更适合用来复习
> 2. 顺序也可能不对，学到哪记到哪，就是这么任性
> 
<div class="shicao">
<form action="">
	*下面只要是实线框包住的部分都是可以实际操作的示例，源代码都会附在框下面<br>
    乖，首先输入你的名字(*ﾟ∀ﾟ*)<br>
    <input type="text" id="lxz" value="#旅行者"><br>
    <button type="button" id="buttonx" onclick="welcomeU()"> 很好，然后点我(ﾉ)`ω´(ヾ) </button><br>
</form>
</div>

<script type="text/javascript">
    var lxzv = document.getElementById("lxz");
    function welcomeU(){
        alert('             \\\\\\'+lxzv.value+'/// \n 举高高(ノﾟ∀ﾟ)ノ');
    }
</script>

## 预解析

- 情况一

  ```
  console.log(num);
  var num = 10；
  ```

  打印：undefined

- 情况二

  ```
  fun();
  function fun(){
  	console.log(10);
  }
  ```

  不报错，正常

- 情况三

  ```
  fun();
  var fun = function(){
  	console.log(10);
  }
  ```

  报错

原因：js 引擎会把 js 里所有 var 和 function 提升到当前作用域的最前面，然后才按照从上往下的顺序执行

- 解释情况一：变量提升只提升声明部分，不提升赋值
- 解释情况二：函数提升只提升声明部分，不调用函数
- 解释情况三：函数表达式，只提升定义，故报错

#坑：

```
var a = b = c = 9;
```

这个相当于 var a = 9; b = 9; c = 9;

b 和 c 没有 var，相当于全局变量。

集体声明应该是：var a = 9, b = 9, c = 9;

## 对象和事件

1. 调用对象的属性的两种方法：
   
    1. 对象名.方法名
    2. 对象名[‘方法名’]
    
    new 的四个步骤：
    
    1. 内存中创建新对象
    2. 让this指向这个新对象
    3. 执行构造函数内的代码，给新对象添加属性和方法
    4. 返回这个新对象（所以构造函数里不需要return

2. 字符串不可变：字符串所有的方法，都不会改变字符串本身，而是返回一个新的字符串对象
3. 字符串查找某字母出现位置和次数：

    <div class="shicao">
    <form action="">
        输入字符串:<br>
        <input type="text" id="str1" value="abccbaabc"><br>
        输入要查找的字母:<br>
        <input type="text" id="str2" value="a"><br>
        <button type="button" id="button1"> 点我查找！</button><br>
        查找结果:<br>
        <textarea style="height:20px;width:300px;word-break:break-all" id="str3" ></textarea>
    </form>
    </div>

    <script type="text/javascript">
        var button1 = document.getElementById('button1');
        button1.onclick = function findstr(){
            var var1 = document.getElementById('str1').value;
            var var2 = document.getElementById('str2').value;
            var var3 = '出现的位置是：';
            var index = var1.indexOf(var2);
            var num = 0;
            while (index != -1){
                var3 = var3 + index + ' ';
                num ++;
                index = var1.indexOf(var2,index+1);
            }
            var3 = var3 + '出现次数是：' + num;
            document.getElementById('str3').value = var3;
        }
    </script>

    ```html
        <div>
            <form action="">
            输入字符串:<br>
            <input type="text" id="str1" value="abccbaabc"><br>
            输入要查找的字母:<br>
            <input type="text" id="str2" value="a"><br>
            <button type="button" id="button1">
                点我查找！
            </button><br>
            查找结果:<br>
            <textarea style="height:20px;width:300px;word-break:break-all" id="str3" ></textarea>
            </form>
        </div>

        <script type="text/javascript">
        var button1 = document.getElementById('button1');
        button1.onclick = function findstr(){
                var var1 = document.getElementById('str1').value;
                var var2 = document.getElementById('str2').value;
                var var3 = '出现的位置是：';
                var index = var1.indexOf(var2);
                var num = 0;
                while (index != -1){
                    var3 = var3 + index + ' ';
                    num ++;
                    index = var1.indexOf(var2,index+1);
                }
                var3 = var3 + '出现次数是：' + num;
                document.getElementById('str3').value = var3;
            }
        </script>
    ```

4. 字符串三个方法：

    返回字符串里某个位置的字符：

    str.charAt(index);

    str[index];（html5新增）

    返回字符串里某个位置的字符的ASCII码值：

    str.charCodeAt(index);

5. 判断字符串里出现次数最多的字符并统计次数：

    <div class="shicao">
        <form action="">
            输入字符串:<br>
            <input type="text" id="chars" value="aaaabbbccd"><br>
            <button type="button" id="button2">
                点我统计！
            </button><br>
            统计结果:<br>
            <textarea style="height:20px;width:300px;word-break:break-all" id="str4" ></textarea>
        </form>
    </div>
    <script type="text/javascript">
            var button2 = document.getElementById('button2');
            button2.onclick = function maxstr(){
                var chars = document.getElementById('chars').value;
                var var4 = '出现最多的字母是：';
                var o = {};
                for (var i = 0 ; i < chars.length ; i++){
                    var chr = chars.charAt(i);
                    if (o[chr]){
                        o[chr] ++;
                    }else{
                        o[chr] = 1;
                    }
                }
                var max = 0;
                var ch = '';
                for (var k in o){
                    if (o[k] > max){
                        max = o[k];
                        ch = k;
                    }
                }
                var4 = var4 + ch + ' 出现次数是：' + max;
                document.getElementById('str4').value = var4;
            }
    </script>

    ```html
        <div>
            <form action="">
            输入字符串:<br>
            <input type="text" id="chars" value="aaaabbbccd"><br>
            <button type="button" id="button2">
                点我统计！
            </button><br>
            统计结果:<br>
            <textarea style="height:20px;width:300px;word-break:break-all" id="str4" ></textarea>
            </form>
        </div>
        <script type="text/javascript">
        var button2 = document.getElementById('button2');
        button2.onclick = function maxstr(){
                var chars = document.getElementById('chars').value;
                var var4 = '出现最多的字母是：';
                var o = {};
                for (var i = 0 ; i < chars.length ; i++){
                    var chr = chars.charAt(i);
                    if (o[chr]){
                        o[chr] ++;
                    }else{
                        o[chr] = 1;
                    }
                }
                var max = 0;
                var ch = '';
                for (var k in o){
                    if (o[k] > max){
                        max = o[k];
                        ch = k;
                    }
                }
                var4 = var4 + ch + ' 出现次数是：' + max;
                document.getElementById('str4').value = var4;
            }
        </script>
    ```

6. 堆和栈

    简单数据类型存放到栈里；操作系统自动分配释放。

    复杂数据类型（引用类型，通过new关键字创建的对象，如Object、Array、Date等）先在栈里存放一个地址，然后实际对象实例存放到堆里；程序员操作分配释放，垃圾回收器回收。

7. 打印元素和方法

    ```javascript
    var timer = document.getElementById('time');
    console.dir(timer);
    ```

8. 弱类型语言，只有一种变量类型：var

    可以不写句尾分号、字符串可以用单/双引号。

    输出并换行：`document.write(sum+"<br>");`

9. DOM：document object model

    节点=标签=元素

    获取特殊元素（body和html）：

    document.body

    document.documentElement

10. 数组 .pop .push .shift .unshift 给尾/头删除/添加元素

11. 对象 Object.keys(对象名)可以返回对象所有的keys，以数组格式

12. 构造函数名字首字母大写；构造函数不需要return；

13. 遍历对象属性：for in循环

    ```javascript
      for (var k in obj) {
      	console.log(k);//得到属性名
      	console.log(obj[k]);//得到属性值
      } 
    ```

14. 执行事件步骤：

    事件三要素：获取事件源（getElementById）-绑定事件（.onclick）-事件处理程序

    <div class="shicao">
    <button id="button3">
        唐伯虎
    </button>
    </div>
    <script>
    	var btn = document.getElementById("button3");
        btn.onclick = function(){
            alert('点秋香');
        }
    </script>

    ```html
    <button id="button3">
        唐伯虎
    </button>
    <script>
        var btn = document.getElementById("button3");
        tn.onclick = function(){
            alert('点秋香');
        }
    </script>
    ```

15.  表单隔行变色高亮以及全选、取消全选实例：

     1.  全选和取消全选：让下面复选框的checked属性跟随上面全选按钮
     2.  下面全选的时候，上面复选框自动选中：每次点击下面复选框，都检查一遍是否全部选中，用flag标注

     <div>
         <table style="width: 300px; margin: 100px auto; text-align: center; border-collapse: collapse; font-size: 14px;">
             <thead>
                 <tr style="height: 30px; background-color: skyblue;">
                     <th>
                         <input type="checkbox" id="j_cbAll" />
                     </th>
                     <th>省分</th>
                     <th>地市</th>
                 </tr>
             </thead>
             <tbody id="j_tb">
                 <tr style="height: 30px;">
                     <td>
                         <input type="checkbox" />
                     </td>
                     <td>山西省</td>
                     <td>太原市</td>
                 </tr>
                 <tr style="height: 30px;">
                     <td><input type="checkbox" />
                     </td>
                     <td>江苏省</td>
                     <td>南京市</td>
                 </tr>
                 <tr style="height: 30px;">
                     <td>
                         <input type="checkbox" />
                     </td>
                     <td>安徽省</td>
                     <td>合肥市</td>
                 </tr>
             </tbody>
         </table>
     </div>
     <script>
         //隔行变色
         var trs = document.querySelector('tbody').querySelectorAll('tr');
         for(var i = 0; i < trs.length; i++){
             trs[i].onmouseover = function(){
                 this.style.backgroundColor = "pink";
             }
             trs[i].onmouseout = function(){
                 this.style.backgroundColor = "";
             }
         }
         //全选按钮
         var j_cbAll = document.getElementById('j_cbAll');
         //下面所有复选框
         var j_tbs = document.getElementById('j_tb').getElementsByTagName('input');
         j_cbAll.onclick = function(){
             for (var i = 0; i < j_tbs.length; i++){
                 j_tbs[i].checked = this.checked;
             }
         }
         for(var i = 0; i < j_tbs.length; i++){
             j_tbs[i].onclick = function(){
                 var flag = true;
                 for(var i = 0; i < j_tbs.length; i++){
                     if(!j_tbs[i].checked){
                         flag = false;
                         break;
                     }
                 }
                 j_cbAll.checked = flag;
             }
         }
     </script>

     ```html
     <div>
         <table style="width: 300px; margin: 100px auto; text-align: center; border-collapse: collapse; font-size: 14px;">
             <thead>
                 <tr style="height: 30px; background-color: skyblue;">
                     <th>
                         <input type="checkbox" id="j_cbAll" />
                     </th>
                     <th>省分</th>
                     <th>地市</th>
                 </tr>
             </thead>
             <tbody id="j_tb">
                 <tr style="height: 30px;">
                     <td>
                         <input type="checkbox" />
                     </td>
                     <td>山西省</td>
                     <td>太原市</td>
                 </tr>
                 <tr style="height: 30px;">
                     <td><input type="checkbox" />
                     </td>
                     <td>江苏省</td>
                     <td>南京市</td>
                 </tr>
                 <tr style="height: 30px;">
                     <td>
                         <input type="checkbox" />
                     </td>
                     <td>安徽省</td>
                     <td>合肥市</td>
                 </tr>
             </tbody>
         </table>
     </div>
     <script>
         //隔行变色
         var trs = document.querySelector('tbody').querySelectorAll('tr');
         for(var i = 0; i < trs.length; i++){
             trs[i].onmouseover = function(){
                 this.style.backgroundColor = "pink";
             }
             trs[i].onmouseout = function(){
                 this.style.backgroundColor = "";
             }
         }
         //全选按钮
         var j_cbAll = document.getElementById('j_cbAll');
         //下面所有复选框
         var j_tbs = document.getElementById('j_tb').getElementsByTagName('input');
         j_cbAll.onclick = function(){
             for (var i = 0; i < j_tbs.length; i++){
                 j_tbs[i].checked = this.checked;
             }
         }
         for(var i = 0; i < j_tbs.length; i++){
             j_tbs[i].onclick = function(){
                 var flag = true;
                 for(var i = 0; i < j_tbs.length; i++){
                     if(!j_tbs[i].checked){
                         flag = false;
                         break;
                     }
                 }
                 j_cbAll.checked = flag;
             }
         }
     </script>
     ```

16. 

## 不会分类了

1. 文档页面从上往下加载，要先写标签，后写script标签

2. IE9以上支持HTML5

3. 根据类名得到元素：document.getElementsByClassName

   返回指定选择器的第一个元素对象document.querySelector('.box')/('#navId');

   返回指定选择器的所有元素对象集合document.querySelectorAll();

   注意querySelectorAll()切记加符号，类.ID#标签不加

4. 修改普通盒子、标签等元素内容 div.innerText();

   div.innerText()不识别HTML标签，且不识别空格和换行

   div.innerHTML()识别HTML标签，w3c标准推荐

   这两个都是可读写的，可以元素的获取内容

5. JS写的样式会嵌入到行内样式，权重高于引入的css文件；

   element.style              行内样式操作，适合样式修改较少的情况

   element.className  类名样式操作，想保留原先的类名的话，可以同时写两个类名空格隔开

## 基础补一补

1. 输出语句

    ```
    alert("要输出的内容");  
    ```

    该语句会在浏览器窗口中弹出一个警告框

    ```
    document.write("要输出的内容");  
    ```

    该内容将会被写到body标签中，并在页面中显示

    ```
    console.log("要输出的内容");  
    ```

    该内容会被写到开发者工具的控制台中

2. 分号

    ```
    function functionName(arg0,arg1,arg2){  
    //函数声明  
    }  
    var functionName=function(arg0,arg1,arg2){  
    //函数表达式  
    };(注意分号)  
    ```

    函数声明不需要分号，但是赋值语句要加分号

3. 数据类型

    **JS中一共分成六种数据类型：5个基本数据类型+object对象**：  

    String 字符串、Number 数值、Boolean 布尔值、Null 空值（typeof检查会显示为object；没有方法，强转数字变为0）、Undefined 未定义（没有方法，强转数字变为NaN）、Object 对象

    **基本数据类型的数据，变量是直接保存的它的值。**

    变量与变量之间是互相独立的，修改一个变量不会影响其他的变量。

    **引用数据类型的数据，变量是保存的对象的引用（内存地址）。**

    如果多个变量指向的是同一个对象，此时修改一个变量的属性，会影响其他的变量。

    比较两个变量时，对于基本数据类型，比较的就是值，

    对于引用数据类型比较的是地址，地址相同才相同

4. 引号和转义字符

    JS中的字符串需要使用引号引起来，双引号或单引号都行

    在字符串中使用\作为转义字符

    ```
    \'  ==> '  
    \"  ==> "  
    \n  ==> 换行  
    \t  ==> 制表符  
    \\  ==> \	  
    ```

5. 特殊的数字：（能赋值给变量，a = Infinity;）

   Infinity 正无穷

   -Infinity 负无穷

   NaN 非法数字（Not A Number）

   其他进制的数字的表示：

   0b 开头表示二进制，但是不是所有的浏览器都支持

   0 开头表示八进制

   0x 开头表示十六进制

6. 强制类型转换

   1. 调用String()函数，等同于 任意数据类型 + “”

      对于Number Boolean String都会调用他们的toString()方法来将其转换为字符串

      对于null值，直接转换为字符串"null"。对于undefined，直接转换为字符串"undefined"。

   2. 调用Number()函数，等同于 + 任意数据类型 

   3. 调用parseInt()或parseFloat()

      这两个函数专门用来将一个字符串转换为数字的，如果对非String使用parseInt()或parseFloat()，它会**先将其转换为String**然后在操作 parseInt()，可以将**一个字符串中的开头的有效的整数位**提取出来，并转换为Number

   4. 调用Boolean()函数，除了空字符串、0、NaN、null、undefined，其余都是true。等同于!!任意数据类型

7. 比较相等的坑

   null == undefined 会返回true（类型不同会作类型转换，undefined衍生自null）

   但是 null === undefined 会返回false（全等不做类型转换）

   NaN不与任何值相等，包括它自身 NaN == NaN

   所以判断一个值是否是NaN，需要使用isNaN()函数

8. 函数：是对象，有属性，使用typeof检查一个函数时会返回 function

   函数声明

   ```
   function 函数名([形参1,形参2...形参N]){  
   语句...  
   }  
   ```

   函数表达式

   ```
   var 函数名 = function([形参1,形参2...形参N]){  
   语句...  
   };  
   ```

9. 函数的属性和方法

   call()、apply()

   **这两个方法都是函数对象的方法，需要通过函数对象来调用**

   通过两个方法可以直接调用函数，并且**可以通过第一个实参来指定函数中this**

   不同的是call是直接传递函数的实参，而apply需要将实参封装到一个数组中传递

10. **arguments**

    arguments和this类似，都是函数中的隐含的参数

    arguments是一个类数组元素，它用来封装函数执行过程中的实参

    所以即使不定义形参，也可以通过arguments来使用实参

    **arguments中有一个属性callee表示当前执行的函数对象**

11. this（调用函数的那个对象）

    this是函数的上下文对象，每次调用函数时，解析器都会将一个上下文对象作为隐含的参数传递进函数。

    根据函数的调用方式不同会执向不同的对象：

    1.以函数的形式调用时，this是window
    2.以方法的形式调用时，this是调用方法的对象
    3.以构造函数的形式调用时，this是新建的那个对象
    4.使用call和apply调用时，this是指定的那个对象
    5.在全局作用域中this代表window

12. 作用域

    - 全局作用域

        直接在script标签中编写的代码都运行在全局作用域中

        **全局作用域在打开页面时创建，在页面关闭时销毁。**

        全局作用域中有一个全局对象window，window对象由浏览器提供，

        可以在页面中直接使用，它代表的是整个的浏览器的窗口。

        **在全局作用域中创建的变量都会作为window对象的属性保存**

        在全局作用域中创建的函数都会作为window对象的方法保存

        在全局作用域中创建的变量和函数可以在页面的任意位置访问。

        在函数作用域中也可以访问到全局作用域的变量。

        尽量不要在全局中创建变量

    - 函数作用域

        函数作用域是函数执行时创建的作用域，每次调用函数都会创建一个新的函数作用域。

        函数作用域在函数执行时创建，在函数执行结束时销毁。

        在函数作用域中创建的变量，不能在全局中访问。

        当在函数作用域中使用一个变量时，它会先在自身作用域中寻找，

        如果找到了则直接使用，如果没有找到则到上一级作用域中寻找，重复此过程。

13. 构造函数

    构造函数是专门用来创建对象的函数，**一个构造函数我们也可以称为一个类**

    通过一个构造函数创建的对象，我们称该对象是这个构造函数的实例

    通过同一个构造函数创建的对象，我们称为一类对象

    构造函数就是一个普通的函数，只是他的调用方式不同，如果直接调用，它就是一个普通函数，如果使用new来调用，则它就是一个构造函数

    例子：

    ```
    function Person(name , age , gender){  
        this.name = name;  
        this.age = age;  
        this.gender = gender;  
        this.sayName = function(){  
            alert(this.name);  
        };  
    }  
    ```

    构造函数的执行流程：

    1.创建一个新的对象
    2.将新的对象作为函数的上下文对象（this）
    3.执行函数中的代码
    4.将新建的对象返回

    `instanceof 用来检查一个对象是否是一个类的实例`

    语法：对象 instanceof 构造函数

    如果该对象是构造函数的实例，则返回 true，否则返回 false

    **Object 是所有对象的祖先，所以任何对象和 Object 做 instanceof 都会返回 true**

    枚举对象中的属性

    `for...in`

    语法：

    ```
    for(var 属性名 in 对象){  
      
    }  
    ```

    for...in语句的循环体会执行多次，对象中有几个属性就会执行几次，每次将一个属性名赋值给我们定义的变量，我们可以通过它来获取对象中的属性

14. 原型（prototype）

    创建一个函数以后，**解析器都会默认在函数中添加一个属性 prototype**

    prototype属性指向的是一个对象，这个对象我们称为原型对象。

    当函数作为构造函数使用，**它所创建的对象中都会有一个隐含的属性执行该原型对象。**

    ```
    这个隐含的属性可以通过对象.__proto__来访问。  
    ```

    **原型对象就相当于一个公共的区域，凡是通过同一个构造函数创建的对象他们通常都可以访问到相同的原型对象。**

    我们可以将对象中共有的属性和方法统一添加到原型对象中，

    这样我们只需要添加一次，就可以使所有的对象都可以使用。

    当我们去访问对象的一个属性或调用对象的一个方法时，它会先自身中寻找，

    如果在自身中找到了，则直接使用。

    如果没有找到，则去原型对象中寻找，如果找到了则使用，

    **如果没有找到，则去原型的原型中寻找，依此类推，直到找到Object的原型为止**。

    **Object的原型的原型为null。如果依然没有找到则返回undefined**。

    `hasOwnProperty()`

    这个方法可以用来检查\**对象自身中**是否含有某个属性

    语法：对象.hasOwnProperty("属性名")

15. 垃圾回收（GC）

    当一个对象没有任何的变量或属性对它进行引用，此时我们将永远无法操作该对象，

    此时这种对象就是一个垃圾，这种对象过多会占用大量的内存空间，导致程序运行变慢，所以这种垃圾必须进行清理。

    在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，

    我们不需要也不能进行垃圾回收的操作，只要将不再使用的对象设置null即可

16. 数组（Array）

    数组也是一个对象，是一个用来存储数据的对象。和 Object 类似，但是它的存储效率比普通对象要高

    数组中保存的内容我们称为元素

    数组使用索引（index，指由0开始的整数）来操作元素

    - 数组的操作：

      创建数组

      语法：

      ```
      var arr = new Array();  
      var arr = [];  
      ```

    - 向数组中添加元素

      语法：数组对象[索引] = 值;

      ```
      arr[0] = 123;  
      arr[1] = "hello";  
      ```

    - 创建数组时直接添加元素

      语法：

      ```
      var arr = [元素1,元素2....元素N]; 
      ```

      例子：

      ```
      var arr = [123,"hello",true,null];  
      ```

    - 获取和修改数组的长度

      使用length属性来操作数组的长度

      1. 获取数组的长度：数组.length

         length获取到的是数组的最大索引+1

         对于连续的数组，length获取到的就是数组中元素的个数

      2. 修改数组的长度：数组.length = 新长度

         如果修改后的length大于原长度，则多出的部分会空出来

         如果修改后的length小于原长度，则原数组中多出的元素会被删除

    - 向数组的最后添加元素

        数组[数组.length] = 值;

    - 数组的方法

      | functionName | function                                                     |   usage                              |
      | ------------ | ------------------------------------------------------------ |   ---------------------------------- |
      | push()       | 用来向数组的末尾添加一个或多个元素，并返回数组新的长度       | 语法：数组.push(元素1,元素2,元素N) |
      | pop()        | 用来删除数组的最后一个元素，并返回被删除的元素               |                                    |
      | unshift()    | 向数组的开头添加一个或多个元素，并返回数组的新的长度         |                                    |
      | shift()      | 删除数组的开头的一个元素，并返回被删除的元素                 |                                    |
      | reverse()    | 可以用来反转一个数组，它会对原数组产生影响                   |                                    |
      | concat()     | 可以连接两个或多个数组，它不会影响原数组，而是新数组作为返回值返回 |                                    |
    
      slice(start,[end])
    
      >  可以从一个数组中截取指定的元素  
      >  该方法不会影响原数组，而是将截取到的内容封装为一个新的数组并返回  
      >  参数：  
      >  	1.截取开始位置的索引（包括开始位置）  
      >  	2.截取结束位置的索引（不包括结束位置）  
      >  第二个参数可以省略不写，如果不写则一直截取到最后  
      >  参数可以传递一个负值，如果是负值，则从后往前数  
    
      splice()
    
      >  可以用来删除数组中指定元素，并使用新的元素替换  
      >  	该方法会将删除的元素封装到新数组中返回  
      >  参数：  
      >  	1.删除开始位置的索引  
      >  	2.删除的个数  
      >  	3.三个以后，都是替换的元素，这些元素将会插入到开始位置索引的前边  
    
      join([splitor])
    
      > 可以将一个数组转换为一个字符串
      >
      > 需要一个字符串作为参数，这个字符串将会作为连接符来连接数组中的元素
      >
      > 如果不指定连接符则默认使用,
    
      sort()
    
      > 可以对一个数组中的内容进行排序，默认是按照Unicode编码进行排序
      >
      > 调用以后，会直接修改原数组。
      >
      > 我们可以自己来指定排序的规则:
      >
      > 我们可以在sort()添加一个回调函数，来指定排序规则，
      >
      > 回调函数中需要定义两个形参,
      >
      > 浏览器将会分别使用数组中的元素作为实参去调用回调函数
      >
      > 使用哪个元素调用不确定，但是肯定的是在数组中a一定在b前边
      >
      > - 浏览器会根据回调函数的返回值来决定元素的顺序，
      >
      >   如果返回一个大于0的值，则元素会交换位置
      >
      >   如果返回一个小于0的值，则元素位置不变
      >
      >   如果返回一个0，则认为两个元素相等，也不交换位置
      >
      > - 如果需要升序排列，则返回 a-b
      >
      >   如果需要降序排列，则返回 b-a
      >
      > ```
      > function(a,b){  
      > 	//升序排列  
      > 	//return a-b;  
      > 
      > 	//降序排列  
      > 	return b-a;  
      > }  
      > ```
  
17. 遍历数组

    遍历数组就是将数组中元素都获取到

    一般情况我们都是使用for循环来遍历数组

    ```
    for(var i=0 ; i<数组.length ; i++){  
        //数组[i]  
    }  
    ```

    使用forEach()方法来遍历数组（不兼容IE8）

    ```
    数组.forEach(function(value , index , obj){  
      
    });  
    ```

    forEach()方法需要一个回调函数作为参数，

    数组中有几个元素，回调函数就会被调用几次，

    每次调用时，都会将遍历到的信息以实参的形式传递进来，

    我们可以定义形参来获取这些信息。

    > value:正在遍历的元素
    >
    > index:正在遍历元素的索引
    >
    > obj:被遍历对象

18. arguments 存储了所有传递过来的实参，是个**伪数组**：1、具有length属性 2、按照索引方式存储，有索引号 3、没有真正数组的方法（push、pop等）

18. 学习中



## 唠叨环节

🤺看到这里的人速速与我击剑🤺

🤺锐利的剑，锐利的眼🤺

## TODO LIST

1. 持续学习中……
2. 更新日期记录：
   1. 20220109
   2. 20220212
   3. 20220311

## 参考内容

[JavaScript基础语法-黑马前端](https://www.bilibili.com/video/BV1Sy4y1C7ha?p=1) 