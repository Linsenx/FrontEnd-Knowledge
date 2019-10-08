# JavaScript DOM选择器函数的比较

## 第一类方法
* document.getElementById()
* document.getElementsByName()
* document.getElementsByTagName()
* document.getElementsByClassName()

## 第二类方法
* document.querySelector()
* document.querySelectorAll()

## 区别
1. ::第一类方法::的::性能::比第二类::好::
2. 第一类获取到的是元素的动态（DOM元素增、删后，集合元素也会动态增、删）集合，第二类获取到的是静态集合（快照）
> 第一类方法获取到的是DOM结构的缓存，第二类获取到的是DOM结构的快照。  
> 第二类方法需要先对CSS选择器进行解析，更耗费性能。  