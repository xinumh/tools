# 手写

改变this指向
``` js
function bindThis(f, oTarget) {
    return f.bind(oTarget)
    //return function () {
    //    return f.apply(oTarget, arguments)
    //}
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
