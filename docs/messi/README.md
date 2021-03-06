---
title: es6面试
---

#### JS如何实现继承？
##### 用prototype实现继承

```js
function Person() {
  this.body = "body";
}
Person.prototype.move = function () {};

function Player(name) {
  this.name = name;
  //自身属性的继承
  Person.apply(this, arguments);
}
//Player.prototype.__proto__ = Person.prototype
//原型属性的继承
var f = function () {};
f.prototype = Person.prototype;
Player.prototype = new f();

Player.prototype.shot = function () {};
var messi = new Player('messi');
console.log(messi);
```

![1635472978(1).png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/10a59c9c3d2a4088a829563ccb152e03~tplv-k3u1fbpfcp-watermark.image?)


##### 用class实现继承的小demo


```js
class Person {
  constructor(name) {
    this.name = name
  }
  eat() { }
}

class FootballPlay extends Person {
  constructor(name, team) {
    super(name)
    this.team = team
  }
  shot() { }
}

let star = new FootballPlay("本泽马","法国")

console.log(star)
console.log(star.shot())
```

![1635473086(1).png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/65b300ac4409458bbb554d1f3758fd23~tplv-k3u1fbpfcp-watermark.image?)


#### Array.prototype.forEach()和Array.prototype.map()的区别
相同点：每次循环的匿名函数都有三个参数（1.数组当前项item 2.当前项的索引index 3.原始数组）

区别：forEach没有返回值，回调函数中可以直接修改原数组的值。而map返回新数组，原数组不变。
```js
let arr = [1, 2, 3, 4, 5];
arr.forEach((num, index) => {
    return arr[index] = num * 2;
});
// arr = [2, 4, 6, 8, 10]
```

#### JavaScript 函数防抖
作用：防止用户在短时间内，大量、高频的重复点击按钮等，导致触发大量请求。

应用场景：比如用户注册

```js
<h1>js防抖</h1>

<input id="btnId" type="button" value="add按钮">
<h2 id="numId">数字</h2>

<script>
    let _btn = document.getElementById('btnId')
    let _n = document.getElementById('numId')
    let _m = 0
    let t = false

    _btn.onclick = function() {
        //重置回初始化的状态
        clearTimeout(t)
        t = setTimeout(function() {
            _n.innerHTML = ++_m
        },500) 
    }
</script>
```

#### JavaScript宏任务和微任务
宏是一种批量处理的称谓。

1.宏任务：script、setTimeout、setInterval、I/O、DOM渲染、点击事件等

2.微任务：(Promise对象的这些方法).then/catch/finally等

3.执行顺序：主线程>微任务>宏任务

宏任务和微任务都可以异步操作，那微任务解决的问题是？
为了解决主线程任务过多的时候，异步回调等待时间过长的问题。


### Array.from()

将其他数据类型转换成数组

##### 1.基本用法

```js
console.log(Array.from('str'))   //["s","t","r"]
```

##### 2.哪些可以通过Array.from()转换为数组？

所有可遍历的。数组、字符串、Set、Map、NodeList、arguments;

拥有length属性的任何对象

##### 3.第二个参数

作用类似于数组的map方法

```js
console.log(Array.from('12',value => value*2))  //[2, 4]
``` 



### undefined
1.既是一个原始数据类型，也是一个原始值数据

2.undefined是全局对象上的一个属性。window.undefined (不可写，不可配置，不可枚举)

3.系统会给一个未赋值的变量自动赋值为undefined

4.函数内部没有显示返回一个值的时候，系统默认给函数返回undefined

5.undefined不是JS的保留字和关键字
