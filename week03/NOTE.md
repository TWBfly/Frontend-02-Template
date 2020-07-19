学习笔记

##### 什么是拆箱?

将引用类型对象转换为对应的基本类型

```
toString() 
valueOf() 
Symbol.toPrimitive(),优先Symbol.toPrimitive()
```

##### 什么是toPrimitive?

 ```
  - 检查对象中是否有用户显式定义的 [Symbol.toPrimitive] 方法，如果有，直接调用；
  - 如果没有，则执行原内部函数 ToPrimitive，然后判断传入的 hint 值，如果其值为 string，顺序调用对象的 toString 和 valueOf 方法（其中 toString 方法一定会执行，如果其返回一个基本类型值，则返回、终止运算，否则继续调用 valueOf 方法）；
  - 如果判断传入的 hint 值不为 string，则就可能为 number 或者 default 了，均会顺序调用对象的 valueOf 和 toString 方法（其中 valueOf 方法一定会执行，如果其返回一个基本类型值，则返回、终止运算，否则继续调用 toString 方法）；
 ```

##### 什么是装箱?

把基本数据类型转化为对应的引用数据类型的操作

```
都是new    symbol -> new Object(Symbol("a"))
```

##### 预处理机制?

```
所有的声明都是有预处理机制，都能够把变量变成一个局部变量。

const声明，在声明之前使用会报错
```

##### 什么是闭包？

```
MDN文档  https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures
闭包是指有权访问另一个函数作用域中的变量的函数
闭包是由函数以及声明该函数的词法环境组合而成的。该环境包含了这个闭包创建时作用域内的任何局部变量。
```

##### 闭包为什么可以实现在函数外读取到函数内的变量？

```
function f1(){
        var n = 123;
        function f2(){    //f2是一个闭包
            alert(n)
        }    
        return f2;
    }
原因：f1是f2的父函数，f2被赋给了一个全局变量，f2始终存在内存中，f2的存在依赖f1，因此f1也始终存在内存中，不会在调用结束后，被垃圾回收机制回收。

function outFun(){
    var name = "Chrome";
    function alertName(){
        alert(name);
    }
    return alertName;  //alertName被外部函数作为返回值返回了,返回的是一个闭包
}

var myFun = outFun();
myFun();

闭包有函数+它的词法环境；词法环境指函数创建时可访问的所有变量。
myFun引用了一个闭包，闭包由alertName()和闭包创建时存在的“Chrome”字符串组成。
alertName（）持有了name的引用，
myFunc持有了alertName（）的的访问，
因此myFunc调用时，name还是处于可以访问的状态。
 
```

##### js执行机制 宏任务 微任务

<https://juejin.im/post/59e85eebf265da430d571f89>

