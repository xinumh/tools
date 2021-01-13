# 字符串转驼峰格式

> css 中经常有类似 background-image 这种通过 - 连接的字符，通过 javascript 设置样式的时候需要将这种样式转换成 backgroundImage 驼峰格式，请完成此转换功能
> 
> 1. 以 - 为分隔符，将第二个起的非空单词首字母转为大写
> 2. -webkit-border-image 转换后的结果为 webkitBorderImage


## String.prottype.replace

`原字符串不会改变`

返回一个由替换值（replacement）替换部分或所有的模式（pattern）匹配项后的新字符串

> str.replace(regexp|substr, newSubStr|function)

`regexp` (pattern) 正则匹配，匹配内容被第二个参数的返回值替换

`substr` (pattern) 一个将被 newSubStr 替换的 字符串,仅第一个匹配项被替换

`newSubStr` (replacement) 新字符串，可以内插特殊[变量名](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

`function` (replacement) 返回新字符串的函数，正则全局匹配会多次调用函数,如果正则有多个括号，则参数代表第n个括号匹配的字符串。

## 示例

```js
 /**
   * 转换为驼峰格式
   */
  var camelize = function (str) {
    // c为匹配到的（\w）
    return str.replace(/-(\w)/g, function (_, c) {
      return c ? c.toUpperCase() : '';
    })
  };

```
