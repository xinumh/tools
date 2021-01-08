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

String.prottype.replace()

> str.replace(regexp|substr, newSubStr|function)

regexp (pattern) 正则匹配，匹配内容被第二个参数的返回值替换

substr (pattern) 一个将被 newSubStr 替换的 字符串,仅第一个匹配项被替换

newSubStr (replacement) 新字符串，可以内插特殊[变量名](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

function (replacement) 返回新字符串的函数，正则全局匹配会多次调用函数,如果正则有多个括号，则参数代表第n个括号匹配的字符串。

```js
 /**
   * 转换为驼峰格式
   */
  var camelize = function (str) {
    // c为匹配到的（\w）
    return str.replace(/-(\w)/g, function (_, c) { return c ? c.toUpperCase() : ''; })
  };

```

函数珂里化

instanceof

原型继承

[参考地址](https://zhuanlan.zhihu.com/p/268821684)
