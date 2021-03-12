### 字符串转驼峰格式

> css 中经常有类似 background-image 这种通过 - 连接的字符，通过 javascript 设置样式的时候需要将这种样式转换成 backgroundImage 驼峰格式，请完成此转换功能
> 
> 1. 以 - 为分隔符，将第二个起的非空单词首字母转为大写
> 2. -webkit-border-image 转换后的结果为 webkitBorderImage

```js
function cssStyle2DomStyle(sName) {
   return sName.replace(/-(\w)/g, function (_, c, index) {
      if(index === 0) {
        return c
      } else {
        return c ? c.toUpperCase() : ''
      }
   })
}

```

### 数组去重

> 为 Array 对象添加一个去除重复项的方法
> 
> 输入： [false, true, undefined, null, NaN, 0, 1, {}, {}, 'a', 'a', NaN]
> 
> 输出： [false, true, undefined, null, NaN, 0, 1, {}, {}, 'a']

```js
Array.prototype.uniq = function () {
    // return [...new Set(this)]
    let arr = []
    let flag = true
    
    for (let i = 0; i < this.length; i ++) {
        if (arr.indexOf(this[i]) === -1) {
            if (this[i] !== this[i]) {
                if (flag) {
                    arr.push(this[i])
                    flag = false
                } 
            } else {
                arr.push(this[i])
            }
        }
    }
    return arr
}

```

### 改变this指向

> 封装函数 f，使 f 的 this 指向指定的对象

``` js
// m-1
function bindThis(f, oTarget) {
    return f.bind(oTarget)
}
// m-2
function bindThis(f, oTarget) {
    return function () {
       return f.apply(oTarget, arguments)
    }
}

```
### 查找两个节点的最近的共同父节点

> 查找两个节点的最近的一个共同父节点，可以包括节点自身

```js
// M-1
function commonParentNode(oNode1, oNode2) {
    if (oNode1 === oNode2) return oNode1
    if(oNode1.parentNode) {
        return commonParentNode(oNode1.parentNode, oNode2)
    }
    if(oNode2.parentNode) {
        return commonParentNode(oNode2.parentNode, oNode1)
    }
}
// M-2
function commonParentNode(oNode1, oNode2) {
    for(;oNode1;oNode1 = oNode1.parentNode) {
       if(oNode1.contains(oNode2)) {
           return oNode1
       }
    }
}
```

### 获取url中的参数

> 获取 url 中的参数
> 
> 1. 指定参数名称，返回该参数的值 或者 空字符串
> 2. 不指定参数名称，返回全部的参数对象 或者 {}
> 3. 如果存在多个同名参数，则返回数组

```js
function getUrlParam(sUrl, sKey) {
    const obj = {}
    sUrl.replace(/\??(\w+)=(\w+)&?/g, function(_, k, v){
        if(obj[k] !== void(0)) {
            let t = obj[k]
            obj[k] = [].concat(t,v)
        } else {
            obj[k] = v
        }
    })
    if(sKey === void(0)) {
        return obj
    } else {
        return obj[sKey] || ''
    }
}
```

### 按所给的时间格式输出指定的时间

``` js
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

