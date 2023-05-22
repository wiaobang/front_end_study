# 第三周问题及回答

## 学习内容：JS 函数 + 期约与异步函数

***

### Q：箭头函数和普通函数的区别
箭头函数是es6新增语法。任何可以使用函数表达式的地方，都可以使用箭头函数。箭头函数语法：
```js
let arrowSum = (a, b) => { 
 return a + b; 
}; 
let functionExpressionSum = function(a, b) { 
 return a + b; 
}; 

console.log(arrowSum(5, 8)); // 13 
console.log(functionExpressionSum(5, 8)); // 13 
```
如果箭头函数只有一个参数，那也可以不用括号
```js
// 以下两种写法都有效
let double = (x) => { return 2 * x; }; 
let triple = x => { return 3 * x; }; 
```
箭头函数也可以不用大括号，如果不使用大括号，那么箭头后面就只能有一行代码，
比如一个赋值操作，或者一个表达式。而且，省略大括号会隐式返回这行代码的值
```js
// 以下两种写法都有效，而且返回相应的值
let double = (x) => { return 2 * x; }; 
let triple = (x) => 3 * x; 

// 可以赋值
let value = {}; 
let setName = (x) => x.name = "Matt"; 
setName(value); 
console.log(value.name); // "Matt" 

// 无效的写法：
let multiply = (a, b) => return a * b;
```
箭头函数不能使用 arguments、super 和
new.target，也不能用作构造函数。此外，箭头函数也没有 prototype 属性  
箭头函数与普通函数的区别主要在于：
1. 箭头函数不会创建自己的this，所以它没有自己的this，它只会从自己的作用域链的上一层继承this。
箭头函数没有自己的this，它会捕获自己**定义时**所处的**外层执行环境的**this，并继承这个this值。所以，箭头函数中this的指向在它被定义的时候就已经确定了，之后永远不会改变。
    ```js
    var id = 'Global';

    function fun1() {
        // setTimeout中使用普通函数
        setTimeout(function(){
            console.log(this.id);
        }, 2000);
    }

    function fun2() {
        // setTimeout中使用箭头函数
        setTimeout(() => {
            console.log(this.id);
        }, 2000)
    }

    fun1.call({id: 'Obj'});     // 'Global'

    fun2.call({id: 'Obj'});    // 'Obj'
    ```
    函数 fun1 中的 `setTimeout` 中使用普通函数,这时函数其实是在全局作用域执行的，所以`this`指向Window对象，this.id就指向全局变量id，所以输出'Global'。  
    函数 fun2 中的 `setTimeout` 中使用的是箭头函数，这个箭头函数的`this`在定义时就确定了，它继承了它外层fun2的执行环境中的this，而fun2调用时this被call方法改变到了对象`{id: 'Obj'}`中，所以输出'Obj'。  
    箭头函数继承而来的this指向永远不变
    ```js
    var id = 'GLOBAL';
    var obj = {
    id: 'OBJ',
    a: function(){
        console.log(this.id);
    },
    b: () => {
        console.log(this.id);
    }
    };

    obj.a();    // 'OBJ'
    obj.b();    // 'GLOBAL'
    ```
2. 箭头函数不能作为构造函数使用
    ```js
    let Fun = (name, age) => {
        this.name = name;
        this.age = age;
    };

    // 报错
    let p = new Fun('cao', 24);
    ```
3. 箭头函数没有自己的arguments.在箭头函数中访问arguments实际上获得的是外层局部（函数）执行环境中的值。

4. 箭头函数没有原型prototype
    ```js
    let sayHi = () => {
        console.log('Hello World !')
    };
    console.log(sayHi.prototype); // undefined
    ```
### Q：说说闭包

### Q：手写 Promise all