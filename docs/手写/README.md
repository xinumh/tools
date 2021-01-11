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

### 按所给的时间格式输出指定的时间

```js
function formatDate(t, str) {
    const obj = {
        yyyy: t.getFullYear(),
        yy: t.getFullYear().toString().slice(-2),
        MM: ('0' + (t.getMonth() + 1)).slice(-2),
        M: t.getMonth() + 1,
        dd: ('0' + t.getDate()).slice(-2),
        d: t.getDate(),
        HH: ('0' + t.getHours()).slice(-2),
        H: t.getHours(),
        hh: ('0' + t.getHours() % 12).slice(-2),
        h: t.getHours() % 12,
        mm: ('0' + t.getMinutes()).slice(-2),
        m: t.getMinutes(),
        ss: ('0' + t.getSeconds()).slice(-2),
        s: t.getSeconds(),
        w: ['日','一', '二', '三', '四', '五', '六'][t.getDay()]
    }
    return str.replace(/([a-z]+)/ig, (s) => {
        return obj[s]
    })
}

formatDate(new Date(1409894060000), 'yyyy-MM-dd HH:mm:ss 星期w')
// "2014-09-05 13:14:20 星期五"
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

### String.prottype.replace

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

### Number.prototype.toString

> numObj.toString([radix])

`radix`指定要用于数字到字符串的转换的基数(从2到36)。如果未指定 radix 参数，则默认值为 10。

```js
function rgb2hex(sRGB) {
    const rgbRegex = /^rgb\((\s*\d+\s*\,){2}(\s*\d+\s*)\)$/
    const numList = sRGB.match(/\d+/g)
    if(rgbRegex.test(sRGB)) {
        let str = '#'
        for(let i=0; i< numList.length;i++) {
            const num = Number(numList[i])
            if (num <= 255 && num >= 0) {
                // Number.prototype.toString()
                str += num < 16 ? '0' + num.toString(16) : num.toString(16)
            }
        }
        return str
    } else {
        return sRGB
    }
}
rgb2hex('rgb(255, 255, 255)') // #ffffff

```

函数珂里化

instanceof

原型继承

[参考地址](https://zhuanlan.zhihu.com/p/268821684)
