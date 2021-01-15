# vue 异常捕获

- [vue 异常捕获](#vue-异常捕获)
    - [main.js](#mainjs)
    - [axios 拦截](#axios-拦截)
    - [业务代码](#业务代码)
    - [errorHandler](#errorhandler)
    - [unhandlerejection](#unhandlerejection)

### main.js

```js

const errorHandler = (event) => {
  // console.error('异常捕获：', event.reason)
  event.preventDefault()
}

Vue.config.errorHandler = reason => {
  let defaultPrevented = false
  errorHandler({ reason, preventDefault: () => { defaultPrevented = true } })
  console.log('defaultPrevented', defaultPrevented)
  if (!defaultPrevented) throw reason // 拦截reject，不再上报错误
}

window.addEventListener('unhandledrejection', errorHandler)

```

### axios 拦截

```js
service.interceptors.response.use(
  response => {
    // 接收到响应数据并成功后的一些共有的处理，关闭loading等
    const { code, msg } = response.data
    if (code === '0') {
      return response.data
    } else {
      Message.error(msg)
      return Promise.reject(msg)
    }
  },
  error => {
    /** *** 接收到异常响应的处理开始 *****/
    if (error && error.response) {
      // 1.公共错误处理
      // 2.根据响应码具体处理
      switch (error.response.status) {
        case 400:
          error.message = '错误请求'
          break
        case 401:
          // error.message = '未授权，请重新登录'
          loginExit('未授权，请重新登录')
          break
        case 403:
          loginExit('拒绝访问')
          break
        case 404:
          error.message = '请求错误,未找到该资源'
          // window.location.href = '/NotFound'
          break
        case 405:
          error.message = '请求方法未允许'
          break
        case 408:
          error.message = '请求超时'
          break
        case 500:
          error.message = '服务器端出错'
          break
        case 501:
          error.message = '网络未实现'
          break
        case 502:
          error.message = '网络错误'
          break
        case 503:
          error.message = '服务不可用'
          break
        case 504:
          error.message = '网络超时'
          break
        case 505:
          error.message = 'http版本不支持该请求'
          break
        default:
          error.message = `连接错误${error.response.status}`
      }
    } else {
      // 超时处理
      const isTimeout = JSON.stringify(error).includes('timeout')
      error.message(isTimeout ? '服务器响应超时，请刷新当前页' : '连接服务器失败')
    }
    Message.error(error.message)
    /** *** 处理结束 *****/
    // 如果不需要错误处理，以上的处理过程都可省略
    return Promise.reject(error.response)
  }
)
```

### 业务代码

采用 `async / await` 同步写法，异常在axios拦截

```js
async getTableData () {
  this.isLoading = true
  const { data: { list = [], total } } = await API.fetchList(this.searchForm).finally(() => { this.isLoading = false }) // 异常
  // 正常返回
  this.tableData = list
  this.total = total
},

```

### errorHandler

> 指定组件的渲染和观察期间未捕获错误的处理函数。
> 这个处理函数被调用时，可获取错误信息和 Vue 实例。

```js
Vue.config.errorHandler = function (err, vm, info) {
  // handle error
  // `info` 是 Vue 特定的错误信息，比如错误所在的生命周期钩子
  // 只在 2.2.0+ 可用, v-on handler  / render
}
```
局部源码
```js
/*!
 * Vue.js v2.6.12
 * (c) 2014-2020 Evan You
 * Released under the MIT License.
 */
function globalHandleError (err, vm, info) {
  if (config.errorHandler) {
    try {
      return config.errorHandler.call(null, err, vm, info)
    } catch (e) {
      // if the user intentionally throws the original error in the handler,
      // do not log it twice
      if (e !== err) {
        logError(e, null, 'config.errorHandler');
      }
    }
  }
  logError(err, vm, info);
}

function logError (err, vm, info) {
  {
    warn(("Error in " + info + ": \"" + (err.toString()) + "\""), vm);
  }
  /* istanbul ignore else */
  if ((inBrowser || inWeex) && typeof console !== 'undefined') {
    console.error(err);
  } else {
    throw err
  }
}
```

### unhandlerejection

> 当Promise 被 reject 且没有 reject 处理器的时候，会触发 `unhandledrejection` 事件。
>
> `unhandlerejection` 含有 `PromiseRejectionEvent` 和 `Event` 的属性和方法。

默认情况下，会向控制台打印未处理的Promise rejections，可以通过添加程序来防止 `unhandledrejection`这种情况的发生，该程序还可以调用 `preventDefault`来取消该事件，从而防止事件冒泡。

```js
window.addEventListener('unhandledrejection', function (event) {
  // ...您的代码可以处理未处理的拒绝...

  // 防止默认处理（例如将错误输出到控制台）

  event.preventDefault();
});
```