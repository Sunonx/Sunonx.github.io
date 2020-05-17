# Html-Css学习笔记


# 第一章  HTML+CSS

## 优先级

**！importent   >  行内样式    >  id选择器  >  类选择器 >  标签选择器  >  通配符  >   继承**  Uncategorized

## CSS三大重点

盒子模型     浮动     定位

### **盒子模型**

*注意：*

1.当两个div***上下同级相邻***时，div01的外边距margin和div02的margin不会是相加而是重叠，选取**距离相对大**的那个

2.div***嵌套***时，两个div的距离是 内边距和外边距的和，当父级div**没有定义边框border和内边距**时，容易被子级div带着一起下拉，边距发生合并，取大的那个，

*解决方法：*

（1）父级div定义border：**1px  solid   white**；定义为白色，但**容易发生溢出**

（2）父级div加  **overflow：hidden**；//隐藏     其他属性：**auto**  //增加下拉框，一般不用

### **浮动**

- [ ] float：left、right   // 脱离标准流 ，在天上飞，标准和浮动互不干扰

- [ ] 解决缝隙：

  （1）display：inline-black；但仍有一丢丢缝隙

  （2）同时定义为 float

- [ ] 子盒子在父盒子内部浮动

- [ ] 当子盒子在父盒子内部浮动，继续写标准流时，如果标准流和子盒子重叠，即父盒子height为0时

  解决方法（**清除浮动**）：

  （1）overflow：hidden；

  （2）额外标签：在父盒子下面随便定义一个标签，使用较少，一般不使用         eg：

  ```
  <div  style="clear : both"></div>
  ```

    (3)额外标签升级：用CSS定义   在 父级div标签class属性后面再加一个  classfix  属性  定义的CSS样式为

  ```
  <div class="div clearfix">
  	<div></div>
  	<div></div>
  </div>
  
  .clearfix:after{ content:"";display: block;height: 0px;clear: both;visibility: hidden;
  }
  ```

  ## CSS元素属性

  ```
  display: inline-block;标准流变成横向排列方式
  ```

### 定位（position）

static（静态定位，默认）     **绝对定位（**absolute**）      相对定位（**relative**）       固定定位**（fixed）

absolute：相对于浏览器 ，不占空间         relative：相对于子盒子在父盒子中原来应该在的位置，占空间

1.父盒子未定位。子盒子绝对定位相对于浏览器，

2.父盒子定位（绝对，相对都可），子盒子绝对定位相对于父盒子上原本的位置

3.一般父盒子相对定位（relative）------占空间，子盒子绝对定位（absolute）---不占空间，脱标

4.固定定位（fixed）：网页的导航栏，或者恶心的广告，相对于浏览器固定不动的位置

### 待解决问题：导航栏固定问题？

# 第二章   JavaScript

### 1.基本语法

1.引用其他js文件时，内部定义的内容无效，且前面报错，后面不执行，type="text/javascript"  可写可不写，区分大小写

```
var age=29; 
var nextAge=30;
var max=(age>nextAge)?age:nextAge;   //最大值的表达方式
console.log(max);
```

```
console.log(1<<3);   //左移 = 1*（2^3） 二进制的移动  速率快，但一般不用
console.log(29<<3);   //右移 =29/(2^3)  结果精度缺失
```

### 2.数据类型和变量

argument //数组

第一种是`==`比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；

**第二种是`===`比较，它不会自动转换数据类型，如果数据类型不一致，返回`false`，如果一致，再比较。**

由于JavaScript这个设计缺陷，*不要*使用`==`比较，**始终坚持使用`===`比较。**

另一个例外是**`NaN`这个特殊的Number与所有其他值都不相等，包括它自己**：

```
NaN === NaN; // false
```

**唯一能判断`NaN`的方法是通过`isNaN()`函数：**

```
isNaN(NaN); // true
```

最后要注意浮点数的相等比较：

```
1 / 3 === (1 - 2 / 3); // false
```

这不是JavaScript的设计缺陷。**浮点数在运算过程中会产生误差，**因为*计算机无法精确表示无限循环小数*。要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值：

```
Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true
```

null表示空，大多数情况下，我们都应该用`null`。`undefined`表示未定义，仅仅在判断函数参数是否传递的情况下有用。

创建数组的方法

1.[ ]     2.  是通过`Array()`函数实现：

```
new Array(1, 2, 3); // 创建了数组[1, 2, 3]
```

然而，**出于代码的可读性考虑，强烈建议直接使用`[]`。** 

JavaScript对象的**键都是字符串类型，值可以是任意数据类型** 

注意变量只能用`var`申明一次 。

### 3.字符串

转义字符`\`可以转义很多字符，比如`\n`表示换行，`\t`表示制表符，字符`\`本身也要转义，所以`\\`表示的字符就是`\`。

ASCII字符可以以`\x##`形式的十六进制表示，例如：

```
'\x41'; // 完全等同于 'A'
```

还可以用`\u####`表示一个Unicode字符：

```
'\u4e2d\u6587'; // 完全等同于 '中文'
```

由于多行字符串用`\n`写起来比较费事，所以最新的ES6标准新增了一种**多行字符串**的表示方法，用**反引号 ** ... \**** 表示：

```
`这是一个
多行
字符串`; //ESC下面那个   
```

如果有很多变量需要连接，用`+`号就比较麻烦。ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：  **${  }**

```
var name = '小明';
var age = 20;
var message = `你好, ${name}, 你今年${age}岁了!`;
alert(message);
```

### 4.数组

#### 1.**indexOf**   

与String类似，`Array`也可以通过`indexOf()`来搜索一个指定的元素的位置：

```
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1  ********
arr.indexOf('30'); // 元素'30'的索引为2
```

#### 2.slice    

 截取`Array`的部分元素，然后返回一个新的`Array`：

```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```

注意到`slice()`的起止参数包括开始索引，不包括结束索引。

如果不给`slice()`传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个`Array`：

```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```

#### 3.push和pop               

 对应  **unshift**  （数组前面加元素）和**shift**（数组前面删元素）

`push()`向`Array`的末尾添加若干元素，`pop()`则把`Array`的最后一个元素删除掉：

```
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```

```
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```

#### 4.sort

`sort()`可以对当前`Array`进行排序，它会直接修改当前`Array`的元素位置，直接调用时，按照默认顺序排序：

```
var arr = ['B', 'C', 'A'];
arr.sort();
arr; // ['A', 'B', 'C']
```

#### **5.reverse**

**反转**

#### 6.splice

`splice()`方法是修改`Array`的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素： 

```
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

#### 7.concat

连接  

```
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
```

#### 8.in

如果我们要检测`xiaoming`是否拥有某一属性，可以用`**in`操作符**：

```
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
```

**不过要小心，如果`in`判断一个属性存在，这个属性不一定是`xiaoming`的，它可能是`xiaoming`继承得到的：**

```
'toString' in xiaoming; // true
```

因为`toString`定义在`object`对象中，而所有对象最终都会在原型链上指向`object`，所以`xiaoming`也拥有`toString`属性。

要判断一个属性是否是`xiaoming`**自身拥有**的，而不是继承得到的，可以用**`hasOwnProperty()`方法**：

```
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```

注意 ，**遍历时只能用  xiaoming.[i]   不能用 xiaoming . i  (输出的是i的属性，undefined)**

JavaScript把**`null`、`undefined`、`0`、`NaN`**和**空字符串`''`视为`false`**，其他值一概视为`true` 

#### 9.for ... in     * ***

`for`循环的一个变体是`for ... in`循环，它可以把一个对象的所有属性依次循环出来：

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    console.log(key); // 'name', 'age', 'city'
}
```

要过滤掉对象继承的属性，用`hasOwnProperty()`来实现：

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    if (o.hasOwnProperty(key)) {
        console.log(key); // 'name', 'age', 'city'
    }
}
```

由于`Array`也是对象，而它的每个元素的索引被视为对象的属性，因此，`for ... in`循环可以直接循环出`Array`的索引：

```
var a = ['A', 'B', 'C'];
for (var i in a) {
    console.log(i); // '0', '1', '2'
    console.log(a[i]); // 'A', 'B', 'C'
}
```

*请注意*，**`for ... in`对`Array`的循环得到的是`String`而不是`Number`。

#### 10,Map和 set

```
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```

#### 11.iterable

ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

具有`iterable`类型的集合可以通过新的`for ... of`循环来遍历。

是直接使用`iterable`内置的**`forEach`方法**，它接收一个函数，每次迭代就自动回调该函数。 

```
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
```

**for in 循环的是对象的属性 ; for of 循环的是迭代器中的每一个元素**  

```
 var m = new Map();
	m.hehe = "haha";
	m.set("name","wangjie");
	m.set("hehe","dada");
	m.set("hoho","lolo");
	for(var element in m){
		console.log(element); // hehe
	}

	for(var element of m){
		console.log(element); //["name", "wangjie"] ["hehe", "dada"] ["hoho", "lolo"]
	}
```

 forEach中的function中的参数是和位置相关的，第一个参数就是表示array的元素，不能用作其他用途表示。

### 5.函数

函数体内部的语句在执行时，一旦执行到`return`时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。

如果没有`return`语句，函数执行完毕后也会返回结果，只是**结果为`undefined`**。

#### **1.函数定义两种形式**

```
function abs(x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
```

**注意第二种方式按照完整语法需要在函数体末尾加一个`;`，表示赋值语句结束。** 

```
var abs = function (x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
};  //注意 
```



传入的参数比定义的多或少都没有问题，少的话：

```
abs(); // 返回NaN
```

此时`abs(x)`函数的参数`x`**将收到`undefined`，计算结果为`NaN`**。

要避免收到`undefined`，可以对参数进行检查：

```
function abs(x) {
    if (typeof x !== 'number') {          //先判断一下类型
        throw 'Not a number';
    }
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
```

#### 2.`arguments`

它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数  //**需要好好理解**

可以获得调用者传入的所有参数。也就是说，即使函数不定义任何参数，还是可以拿到参数的值： 

```
function foo(x) {
    console.log('x = ' + x); // 10
    for (var i=0; i<arguments.length; i++) {
        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
    }
}
foo(10, 20, 30);
```

**实际上`arguments`最常用于判断传入参数的个数**。你可能会看到这样的写法：

```
// foo(a[, b], c)
// 接收2~3个参数，b是可选参数，如果只传2个参数，b默认为null：
function foo(a, b, c) {
    if (arguments.length === 2) {
        // 实际拿到的参数是a和b，c为undefined
        c = b; // 把b赋给c
        b = null; // b变为默认值
    }
    // ...
}
```

要把中间的参数`b`变为“可选”参数，就只能通过`arguments`判断，然后重新调整参数并赋值。

#### 3.rest

```
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// 结果:
// a = 1
// b = undefined
// Array []
```

rest参数只能写在最后，前面用**`...`标识**，从运行结果可知，传入的参数先绑定`a`、`b`，多余的参数以数组形式交给变量`rest`，所以，不再需要`arguments`我们就获取了全部参数。

如果传入的参数连正常定义的参数都没填满，也不要紧，rest参数会接收一个**空数组**（注意不是`undefined`）。
