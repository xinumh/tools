

## Array.prototype.concat()

`不会更改现有数组`

合并两个或多个数组,返回新数组。

> var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])

`valueN`(可选)：数组/值，省略参数返回调用concat的数组的一个浅拷贝。

## 示例

```js
const arr1 = [1, 2]
const arr2 = [3, 4]
const arr_new = arr1.concat(arr2)

console.log(arr1) // [1, 2]
console.log(arr_new) // [1, 2, 3, 4]
```
