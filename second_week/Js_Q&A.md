# 第二周问题及回答
## 学习内容：JS 变量、作用域与内存 + 基本引用类型
***
### Q：JavaScript 有哪些类型
Answer:
1. undefined类型。 该类型只存在一个值，即为特殊值undefined。 当一个变量使用var 或者 let 声明但没有初始化时，该变量值即为undefined值。
    ```
    let message;  
    console.log(message == undefined); // true
    ```

2. Null类型。 null 值表示一个空对象指针，当给typeof 传一个 null 会返回"object"
    ```
    let car = null;
    console.log(typeof car); // "object"
    ```
    另外，undefined 值是由 null 值派生而来的，ECMA-262 将它们定义为表面上相等
    ```
    console.log(null == undefined); // true
    ```

3. Boolean类型。逻辑类型, 有两个字面值：true 和 false。

4. Number类型。 Number类型字面量包括整数和浮点数。Number类型存在一个特殊的数据NaN，用于表示本来要返回数值的操作失败。 
    - 整数。整数可由十进制、八进制或者十六进制字面量表示。表示八进制字面量，第一个数字必须是零（0），然后是相应的八进制数字（0~7，不大于7）。表示十六进制时，使用0x作为前缀。
        ```
        let intNum = 55; // 整数
        let octalNum1 = 070; // 八进制的 56
        let hexNum1 = 0xA; // 十六进制 10
        ```
    - 浮点数。定义浮点值时，数值中必须包含小数点，而且小数点后面必须至少有一个数字。
        ``` 
        let floatNum2 = 0.1;
        let floatNum1 = 1.; // 小数点后面没有数字，当成整数 1 处理。
        let floatNum3 = 3.125e7; // 科学计数法表示，等于 31250000
        ```
    - NaN值。意思是“不是数值”（Not a Number），用于表示本来要返回数值的操作
失败了（而不是抛出错误）。在 ECMAScript 中，0、+0 或0 相除会返回 NaN。 NaN 不等于包括 NaN 在内的任何值， 可以使用isNaN()函数检测参数是否是数值。
        ```
        console.log(0/0); // NaN
        console.log(NaN == NaN); // false
        console.log(isNaN(NaN)); // true
        console.log(isNaN(10)); // false，10 是数值
        console.log(isNaN("10")); // false，可以转换为数值 10
        console.log(isNaN("blue")); // true，不可以转换为数值
        console.log(isNaN(true)); // false，可以转换为数值 1
        ```
    
5. String类型。 表示零或多个 16 位 Unicode 字符序列。字符串可以使用双引号（"）、单引号（'）或反引号（`）标示。字符串是不可变的（immutable），它们一旦创建，它们的值就不能变了。要修改
某个变量中的字符串值，必须先销毁原始的字符串，然后将包含新值的另一个字符串保存到该变量

6. Symbol类型。 ECMAScript 6 新增的数据类型。符号是原始值，且符号实例是唯一、不可变的。
符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险。

7. Object类型。一组数据和功能的集合。对象可通过 new 操作符后跟对象类型的名称来创建。Object 是派生其他对象的基类。Object 类型的所有属性和方法在派生的对象上同样存在。

### Q: 基本类型和引用类型的区别
Answer:
1. 基本类型：基本类型值指的是简单的数据段,基本数据类型可以直接操作保存在变量中的实际值,主要包括Undifined、Null、Boolean、Number和String。把一个基本类型变量赋值到另一个变量时，变量值会被复制到新变量的位置，两个变量是完全独立的，可以独立使用，互不干扰。
    ```
    let num1 = 5;
    let num2 = num1;
    num2 = 8;
    console.log(num2); // 8
    console.log(num1); // 5
    ```
2. 引用类型：引用数据类型是保存在堆内存中的对象，引用类型的数据，在栈内存中保存的实际上是对象在堆内存中的引用地址。在把引用值从一个变量赋给另一个变量时，存储在变量中的值也会被复制到新变量所在的位置。这里复制的值实际上是一个指针，它指向存储在堆内存中的对象。操作完成后，两个变量实际
上指向同一个对象，因此一个对象上面的变化会在另一个对象上反映出来。
    ```
    let obj1 = new Object();
    let obj2 = obj1;
    obj1.name = "Nicholas";
    console.log(obj2.name); // "Nicholas
    ```

### Q: 如何判断变量类型
Answer:
 1. 基本类型可以通过typeof 操作符进行判断。可以通过typeof 操作符判断一个变量是否为字符串、数值、布尔值或 undefined，但如果值是对象或 null，typeof都将返回"object"。
    ```
    let s = "Nicholas";
    let b = true;
    let i = 22;
    let u;
    let n = null;
    let o = new Object();
    console.log(typeof s); // string
    console.log(typeof i); // number
    console.log(typeof b); // boolean
    console.log(typeof u); // undefined
    console.log(typeof n); // object
    console.log(typeof o); // object
    ```
2. 引用对象的判断可以通过instanceof操作符实现，通过它可以知道引用类型对象是什么类型的对象。
    ```
    console.log(person instanceof Object); // 变量 person 是 Object 吗？
    console.log(colors instanceof Array); // 变量 colors 是 Array 吗？
    console.log(pattern instanceof RegExp); // 变量 pattern 是 RegExp 吗？
    ```
### Q: var let const的区别
Answer:
1. var。 可以通过var关键字定义一个变量，在使用 var 声明变量时，变量会被自动添加到最接近的上下文。var声明的范围是函数作用域，使用 var 操作符定义的变量会成为包含它的函数的局部变量。
    ```
    function test() {
    var message = "hi"; // 局部变量
    }
    test();
    console.log(message); // 出错！
    ```
    使用var关键字声明的变量会自动提升到函数作用域顶部,即变量声明拉到函数作用域的顶部：
    ```
    function foo() {
        console.log(age);
        var age = 26;
    }
    foo(); // undefined
    ```
    其等价于：
    ```
    function foo() {
    var age;
    console.log(age);
    age = 26;
    }
    foo(); // undefined
    ```
2. let。let的作用于var类似。但let声明的范围是块作用域，与var的区别：
    ```
    if (true) {
    var name = 'Matt';
    console.log(name); // Matt
    }
    console.log(name); // Matt

    if (true) {
    let age = 26;
    console.log(age); // 26
    }
    console.log(age); // ReferenceError: age 没有定义
    ```
    let 不允许同一个块作用域中出现冗余声明。这样会导致报错：
    ```
    let age;
    let age; // SyntaxError；标识符 age 已经声明过了
    ```
    对声明冗余报错不会因混用 let 和 var 而受影响。这两个关键字声明的并不是不同类型的变量，
它们只是指出变量在相关作用域如何存在。
    ```
    var name;
    let name; // SyntaxError
    let age;
    var age; // SyntaxError
    ```
    使用 let 在全局作用域中声明的变量不会成为 window 对象的属性，并且let不会进行变量提升。
3. const。const的作用域和let相同。const和let的区别在于用它声明变量时必须同时初始化变量,const声明的变量不能更改。
    ```
    const age = 26;
    age = 36; // TypeError: 给常量赋值
    ```
### Q: 解释一下作用域
Answer: （不严谨）  
在 JavaScript 中，作用域是执行代码的上下文。作用域主要分为全局作用域和函数作用域（也称“局部作用域”）。全局作用域中声明的变量可以在程序的任意位置访问，如果一个变量是在函数内部声明的,它就在局部作用域下,这个变量只能在函数内部访问,不能在函数以外去访问。
```
var color = "blue";
function changeColor() {
let anotherColor = "red";
function swapColors() {
let tempColor = anotherColor;
anotherColor = color;
color = tempColor;
// 这里可以访问 color、anotherColor 和 tempColor
}
// 这里可以访问 color 和 anotherColor，但访问不到 tempColor
swapColors();
}
// 这里只能访问 color
changeColor()
```

### Q: const 定义的值一定不能改变吗？
Answer:  
使用const声明的基本类型的值不能更改，但
const 声明的限制只适用于它指向的变量的引用，如果 const 变量引用的是一个对象，
那么修改这个对象内部的属性并不违反 const 的限制。
```
const person = {};
person.name = 'Matt'; // ok
```