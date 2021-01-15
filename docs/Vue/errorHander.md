# vue 异常捕获

- errorHandler
- unhandledrejection

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