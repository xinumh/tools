# 在数组 arr 的 index 处添加元素 item。不要直接修改数组 arr，结果返回新的数组

> 输入： [1, 2, 3, 4], 'z', 2
>
> 输出： [1, 2, 'z', 3, 4]

``` js
function insert (arr, item, index) {
  const _arr = [].concat(arr)
  list.splice(index, 0, item)
  return list
}
```

## splice()

通过`删除或替换`现有元素或者`原地添加`新的元素来修改数组,并以数组形式返回被修改的内容。此方法会**改变原数组**

## 语法

> array.splice(start[, deleteCount[, item1[, item2[, ...]]]])

`start`,修改的开始位置(从0计数)，`start > length`,则末尾添加；`start < 0`，则从倒数第n个；`负数的绝对值 > length`， 则从0计。

`deleteCount`，可选

`item1, item2, ...`，可选

## 示例


### 从第 n 位插入 元素item
```js
arr.splice(n, 0, item)
// 
```

### 从第 n 位 删除m个元素，插入 元素item
```js
arr.splice(n, m, item)
// 
```

### 从第 n 位 删除m个元素
```js
arr.splice(n, m)
// 
```


### 从倒数第 n 位 删除m个元素
```js
arr.splice(-n, m)
// 
```


### 从第 n 位 删除所有元素
```js
arr.splice(n)
// 
```