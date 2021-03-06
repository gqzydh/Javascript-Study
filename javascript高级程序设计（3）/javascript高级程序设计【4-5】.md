## 目录##

4.[第4章 变量-作用域和内存问题](第四章 变量-作用域和内存问题)

5.[第5章 引用类型](第5章 引用类型)

​	

### 第4章 变量-作用域和内存问题###

##### 1. 基本类型和引用类型的值

> 在将一个值赋给变量时，解析器必须确定这个值是基本类型值还是引用类型值。						

- **基本类型值指的是简单的数据段**: 不能给基本类型的值添加属性


- **引用类型值指那些可能由多个值构成的对象**: 对于引用类型的值，我们可以为其添加属性和方法，也可以改变和删除其属性和方法。

  ```引用类型值
  var person = new Object(); 
  	person.name = "Nicholas"; 
  	alert(person.name); //"Nicholas"
  ```

  ```基本类型值
  var name = "Nicholas";
      name.age = 27;
      alert(name.age);      //undefined
  ```

#### 2.复制变量值

- **复制基本类型的值**: 会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上		

- **复制引用类型的值**:不同的是，这个值的副本实际上是一个指针，而这个指针指向存储在堆中的一个对象。

  ```复制引用类型的值
  var obj1 = new Object();
  var obj2 = obj1;
      obj1.name = "Nicholas";
      alert(obj2.name);  //"Nicholas"
  ```

#### 3.传递参数####

> ECMAScript 中所有函数的参数都是按值传递的。
>
>
> 访问变量有按值和按引用两种方式，而参数只能按值传递。

​	- 在向参数传递引用类型的**值时**

```
 function addTen(num) {
        num += 10;
		return num; 
}
var count = 20;
var result = addTen(count); 
alert(count); //20，没有变化 
alert(result); //30
```

#### 4.检查类型####

- 要检测一个变量是不是基本数据类型，用 `typeof`  操作符

  ```
  var s = "Nicholas";
  var i = 22;
  var b = true;
  var u;
  var n = null;
  var o = new Object();
  alert(typeof s);  //string
  alert(typeof i);  //number
  alert(typeof b);  //boolean
  alert(typeof u);  //undefined
  alert(typeof n);  //object
  alert(typeof o);  //object
  ```

  ​

#### 第5章 引用类型

	1. object 类型

> 在应用程序中存储和传输数据而言，它们确实是非常理想的选择。

- 创建 Object 实例的方式有两种。

  1. 使用 new 操作符后跟 Object 构造函数 `var person = new Object();`

     `var person = {}; //与new Object()相同`

  2. 使用对象字面量表示法 `var person = {    name : "Nicholas",    age : 29};`

   ​

  **JavaScript 也可以使用方括号表示法来访问对象的属性**

  ```
  alert(person["name"]); //"Nicholas" 使用方括号表示法来访问对象的属性
  alert(person.name); //"Nicholas"  使用的都是点表示法
  ```

  > 方括号语法的主要优点是可以通过变量 来访问属性

  ```
  var propertyName = "name"; 
  alert(person[propertyName]); //"Nicholas"
  person["first name"] = "Nicholas";
  ```

2. Array类型

- 创建数组的基本方式有两种。

  1. 使用 Array 构造函数`var clors = new Array();`

  2. 使用数组字面量表示法

     ```
     var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
     var names = [];  // 创建一个空数组
     var values = [1,2,];  // 不要这样!这样会创建一个包含 2 或 3 项的数组
     ```

     在读取和设置数组的值时，要使用方括号并提供相应值的基于 0 的数字索引

     ```
     var colors = ["red", "blue", "green"]; // 定义一个字符串数组
     alert(colors[0]);  // 显示第一项
     colors[2] = "black";  // 修改第三项
     colors[3] = "brown";  // 新增第四项
     ```

     **利用 length 属性也可以方便地在数组末尾添加新项**

     ```
     var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组 
     colors[colors.length] = "black"; //(在位置3)添加一种颜色
     colors[colors.length] = "brown"; //(在位置4)再添加一种颜色
     ```

  3. 转换方法

     所有对象都具有 toLocaleString()、toString()和 valueOf()方法。

     > `toLocaleString()`把数组转换为本地字符串
     >
     > `toString()`方法可把一个逻辑值转换为字符串，并返回结果。
     >
     > `valueOf()`方法可返回 Boolean 对象的原始值。

     - join() 方法只接收一个参数，即用作分隔符的字符串

       ````
       var colors = ["red", "green", "blue"];
           alert(colors.join(","));       //red,green,blue
           alert(colors.join("||"));      //red||green||blue
       ````

  4. 栈方法

     > 栈数据结构的访问规则是 LIFO(后进先出)

     - `push()`	方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。

     - 和`pop()` 方法则从数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。

       ```
       var colors = new Array(); // 创建一个数组
       var count = colors.push("red", "green"); // 推入两项 alert(count); //2
       count = colors.push("black"); // 推入另一项
       alert(count);     //3
       var item = colors.pop(); // 取得最后一项
       alert(item);      //"black"
       alert(colors.length);   //2
       ```

  5. 列队方法

     > 队列数据结构的访问规则是先进先出。

     `shift()` 它能够移除数组中的第一个项并返回该项，同时将数组长度减 1。

     `unshift()`它能在数组前端添加任意个项并返回新数组的长度。

     ```
     var colors = new Array(); //创建一个数组
     var count = colors.push("red", "green"); alert(count);  //2 //推入两项
     count = colors.push("black");  //推入另一项
     alert(count);     //3
     var item = colors.shift(); //取得第一项
     alert(item); //"red" 
     alert(colors.length); //2
     ```

  6. 重排序方法

     `reverse()` 方法会反转数组项的顺序。

     `sort()` 方法按升序排列数组项——即最小的值位于最前面，最大的值排在最后面。

  7. 操作方法

  ​   `concat()`  方法的是一或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中。如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾。

      ​```
      var colors = ["red", "green", "blue"];
          var colors2 = colors.concat("yellow", ["black", "brown"]);
          alert(colors);     //red,green,blue
          alert(colors2);    //red,green,blue,yellow,black,brown
      ​```

    `slice()`方法可以 接受一或两个参数，即要返回项的起始和结束位置

    ```
    var colors = ["red", "green", "blue", "yellow", "purple"];
    var colors2 = colors.slice(1);
    var colors3 = colors.slice(1,4);
    alert(colors2);   //green,blue,yellow,purple
    alert(colors3);   //green,blue,yellow
    ```

  -   `splice()` 主要用途是向数组的中部插入项:删除，插入，替换

    ```
    var colors = ["red", "green", "blue"];  // 删除第一项
    var removed = colors.splice(0,1); 
    alert(colors); // green,blue 
    alert(removed); // red，返回的数组中只包含一项

    removed = colors.splice(1, 0, "yellow", "orange");  // 从位置 1 开始插入两项
    alert(colors); // green,yellow,orange,blue 
    alert(removed); // 返回的是一个空数组

    removed = colors.splice(1, 1, "red", "purple");   // 插入两项，删除一项
    alert(colors); // green,red,purple,orange,blue 
    alert(removed); // yellow，返回的数组中只包含一项
    ```


8. 位置方法

   `indexOf()` 和`lastIndexOf()` 两个方法都接收 两个参数:要查找的项和(可选的)表示查找起点位置的索引

   ```
   var numbers = [1,2,3,4,5,4,3,2,1];
       alert(numbers.indexOf(4));        //3
       alert(numbers.lastIndexOf(4)); //5
       alert(numbers.indexOf(4, 4));     //5
       alert(numbers.lastIndexOf(4, 4)); //3
       
   var person = { name: "Nicholas" };
   var people = [{ name: "Nicholas" }];
   var morePeople = [person];
     alert(people.indexOf(person));     //-1
     alert(morePeople.indexOf(person)); //0
   ```

9. 迭代方法

   >  ECMAScript 5 为数组定义了 5 个迭代方法。每个方法都接收两个参数:要在每一项上运行的函数和 (可选的)运行该函数的作用域对象——影响 this 的值。

   `every():`  `filter():`  `forEach():`  `map():`  `some():` 

   ```
    var numbers = [1,2,3,4,5,4,3,2,1];
        var everyResult = numbers.every(function(item, index, array){
            return (item > 2);
   });
   alert(everyResult); //false
        var someResult = numbers.some(function(item, index, array){
            return (item > 2);
   });
   alert(someResult); //true
   var filterResult = numbers.filter(function(item, index, array){
       return (item > 2);
    });
   alert(filterResult); //[3,4,5,4,3]
   var mapResult = numbers.map(function(item, index, array){
           return item * 2;
       });
       alert(mapResult);  //[2,4,6,8,10,8,6,4,2]
   numbers.forEach(function(item, index, array){
   	//执行某些操作
   });
   ```

10. 归并方法

   > ECMAScript 5 还新增了两个归并数组的方法:reduce()和 reduceRight()。这两个方法都会迭 12 代数组的所有项，然后构建一个最终返回的值。












