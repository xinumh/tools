# 手写

### 改变this指向
``` js
function bindThis(f, oTarget) {
    return f.bind(oTarget)
    //return function () {
    //    return f.apply(oTarget, arguments)
    //}
}
```
### 查找两个节点的最近的共同父节点
```js
function commonParentNode(oNode1, oNode2) {
    //for(;oNode1;oNode1 = oNode1.parentNode) {
    //    if(oNode1.contains(oNode2)) {
    //        return oNode1
    //    }
    //}
    if (oNode1 === oNode2) return oNode1
    if(oNode1.parentNode) { return commonParentNode(oNode1.parentNode, oNode2) }
    if(oNode2.parentNode) { return commonParentNode(oNode2.parentNode, oNode1) }
}
```
手写发布订阅模式

模拟new操作符

模拟实现Array.prototype.reduce

throttle（节流）

debounce（防抖）

Promise

箭头函数

用函数实现useEffect功能

数组扁平化

数组去重

类数组转化为数组

深拷贝

Array.prototype.filter()

Array.prototype.map()

Array.prototype.forEach()

Array.prototype.reduce()

Function.prototype.apply()

Function.prototype.call()

Function.prototype.bind()

函数珂里化

instanceof

原型继承

(参考地址)[https://zhuanlan.zhihu.com/p/268821684]
