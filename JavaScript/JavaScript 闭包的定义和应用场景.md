# JavaScript 闭包的定义和应用场景



## 什么是闭包
MDN：闭包是::函数::和::声明该函数的词法环境::的::组合::。

## 简单的例子
```javascript
function init() {
  var name = "Mozilla"; // name 是一个被 init 创建的局部变量
  function displayName() { // displayName() 是内部函数,一个闭包
    alert(name); // 使用了父函数中声明的变量
  }
  displayName();
}
init();
```
运行代码，成功 alert 显示了 “Mozilla”。`init()`创建了一个局部变量`name`和函数`displayName`。`displayName`是`init()`的内部函数，仅在该函数体内可用。`displayName`可以访问到父函数声明的`name`变量。
这个例子介绍了JS引擎是如何解析函数嵌套中的变量的，词法作用域中使用的域，是::变量在代码中的位置::所决定的。嵌套的函数可以访问其外部声明的变量。

## 稍微改变一下
```javascript
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}
var myFunc = makeFunc();
myFunc();
```
运行代码，任然成功显示””Mozilla”。在上面的例子中，`makeFunc()`执行完毕，我们任然能够访问到变量`name`，这是因为JavaScript的函数会形成闭包，闭包是由函数和声明该函数的环境构成，这个环境包含了::这个闭包创建时能访问到的所有**局部变量**::。
`myFunc`是执行`makeFunc`时创建的`displayName`函数的引用，`displayName`可以访问到它的词法作用域中的变量，所以可以访问到`name`。

## 闭包的应用
### 1.用闭包模拟私有方法
```javascript
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var Counter1 = makeCounter();
var Counter2 = makeCounter();
console.log(Counter1.value()); /* logs 0 */
Counter1.increment();
Counter1.increment();
console.log(Counter1.value()); /* logs 2 */
Counter1.decrement();
console.log(Counter1.value()); /* logs 1 */
console.log(Counter2.value()); /* logs 0 */
```
这个例子中，外部不能直接访问`privateCounter`，只能通过公共方法`value()`来获取`privateCounter`的值。

