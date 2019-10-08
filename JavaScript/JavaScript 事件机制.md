# JavaScript 事件机制


## 什么是事件

HTML元素发生的事情。
一些常用的Javascript的事件：
* change：一个HTML元素被改变
* click：用户点击了一个HTML元素
* mouseover：用户将鼠标移到一个HTML元素上
* mouseout：用户将鼠标离开一个HTML元素
* keydown：用户按下键盘按键
* load：浏览器完成当前页面的加载

## 事件委托
事件委托：将事件委托给一个元素，该元素将接收::其中发生的所有事件::。
一般来讲，会把一个元素或一组元素的事件委托到::它的父层或者更外层元素上::，真正绑定事件的是::外层元素::，当该元素事件响应时，会通过事件冒泡机制冒泡到::外层元素::，被外层元素的绑定事件捕获，从而在外层元素执行函数。

## 事件委托的优点
1. 使用事件委托模式可以::减少代码中使用的事件监听器的数量::，大量的事件监听器会::占用大量的内存::，并且绑定或解绑事件可能会造成内存泄露。
2. 给父元素上绑定事件监听器，即使子元素是之后插入到页面中的，其事件也能被监听到。

## DOM事件流程的三个阶段
1. 捕获阶段：事件从::window逐级向下传递到目标::
2. 目标（民中）阶段：事件::已经到达目标::
3. 冒泡阶段：事件::从目标逐级向上传递到最顶层window::
![](http://image.linsenx.com/blog/2019-10-08-8861DE12-EAD2-47A7-9E91-CF873824AF41.png)

## Event.eventPhase: number
表示当前事件的执行阶段：
`var phase = event.eventPhase;`
eventPhase值为整数值，含义如下：
Event.NONE: 0， 没有事件正在被处理
Event.CAPTURING_PHASE: 1，事件被目标元素的祖先对象处理
Event.AT_TARGET: 2，事件已经抵达目标
Event.BUBBLING_PHASE : 3，事件对象逆向向祖先元素传播

## Event.target: Element
指向事件::触发的元素::。

## Event.currentTarget: Element
指向事件::绑定的元素::。

## Event.preventDefault: function
取消默认动作（如果可取消），::不影响事件的传播::，除非碰到`stopPropagation`或`stopImmediatePropagation`。

## Event.stopPropagation: function
阻止该事件的::事件冒泡::或::事件冒泡::。

## Event.stopImmediatePropagation: function
阻止::事件冒泡::或::事件冒泡::并且**阻止相同事件的其它监听器被调用**。
> 备注：如果有多个相同类型事件的事件监听函数绑定到同一个元素，当该类型的事件触发时，它们会::按照被添加的顺序执行::。如果其中某个监听函数执行了 event.stopImmediatePropagation() 方法，则当前元素::剩下的监听函数将不会被执行::。（注意区别 event.stopPropagation ）  
例子：
```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            p { height: 30px; width: 150px; background-color: #ccf; }
            div {height: 30px; width: 150px; background-color: #cfc; }
        </style>
    </head>
    <body>
        <div>
            <p>paragraph</p>
        </div>
        <script>
         const p = document.querySelector('p')
         p.addEventListener("click", (event) => {
           alert("我是p元素上被绑定的第一个监听函数");
         }, false);

         p.addEventListener("click", (event) => {
           alert("我是p元素上被绑定的第二个监听函数");
           event.stopImmediatePropagation();
           // 执行stopImmediatePropagation方法,阻止click事件冒泡,并且阻止p元素上绑定的其他click事件的事件监听函数的执行.
         }, false);

         p.addEventListener("click",(event) => {
           alert("我是p元素上被绑定的第三个监听函数");
           // 该监听函数排在上个函数后面，该函数不会被执行
         }, false);

         document.querySelector("div").addEventListener("click", (event) => {
           alert("我是div元素,我是p元素的上层元素");
           // p元素的click事件没有向上冒泡，该函数不会被执行
         }, false);
        </script>
    </body>
</html>
```