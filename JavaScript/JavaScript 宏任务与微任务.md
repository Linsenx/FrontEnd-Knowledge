# JavaScript 宏任务与微任务



## 宏任务（macrotask）：
* I/O
* setTimeout
* setInterval
* setImmediate ::Node支持，非浏览器标准方法::
* UI rendering: requestAnimationFrame()  ::仅浏览器::

## 微任务（microtask）：
* promise callback (then finally catch)
* MutationObserver ::仅浏览器::
* process.nextTick ::仅Node::
* -已废弃 Object.observe()- ::仅浏览器::
