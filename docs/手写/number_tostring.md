
# 颜色字符串转换

> 将 rgb 颜色字符串转换为十六进制的形式，如 rgb(255, 255, 255) 转为 #ffffff
> 
> 1. rgb 中每个 , 后面的空格数量不固定
> 2. 十六进制表达式使用六位小写字母
> 3. 如果输入不符合 rgb 格式，返回原始输入

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

## Number.prototype.toString

> numObj.toString([radix])

`radix`指定要用于数字到字符串的转换的基数(从2到36)。如果未指定 radix 参数，则默认值为 10。
