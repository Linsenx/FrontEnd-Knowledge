# JavaScript Array方法归纳


## 会改变原数组的方法（修改器方法）
* Array.copyWithin：浅复制数组的一部分到同一数组中的另一个位置，并返回新数组
* Array.fill：将指定区间的元素值替换为固定的值
* Array.reverse：颠倒元素的顺序
* Array.push
* Array.pop：删除最后一个元素，并返回它
* Array.shift：删除第一个元素，并返回它
* Array.unshift：在数组开头增加一个或多个元素，::返回新数组长度::
* Array.sort：::原地排序::算法对数组进行排序
* Array.splice

## 不会改变原数组的方法（访问方法、迭代方法）
访问方法：
* Array.concat
* Array.includes
* Array.join
* Array.slice
* Array.toString
* Array.toLocaleString
* Array.indexOf
* Array.lastIndexOf
迭代方法：
* Array.forEach
* Array.filter
* Array.map
* Array.reduce
* Array.reduceRight
* Array.entries
* Array.every
* Array.some
* Array.find
* Array.findIndex
* Array.keys
* Array.values
