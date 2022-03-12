# VUE的快速入门
## 前置知识
- 前端工程化
> - 模块化规范
> - webpack
- Promise
### 模块化规范
模块化规范有很多 `ESM`、`commonJS` 等。`ESM` 在项目当中被使用，这里对其简单的说明一下，

`ESM` 模块化规范

a.js
```javascript
export default {
    name: 'aaa'
}
```
b.js
```javascript
export const b = {
    name: 'bbb'
}

// 没有被 export 暴露出去的其他无法被模块引入
const c = {
    name: 'ccc'
}
```
main.js
```javascript
import a from './a.js' 
// 这样是引入 a.js 中的暴露出的 default
// 引入的是 default 部分的时候变量名称可以是任意的
//     import c from './a.js' ✔️

import { b } from './b.js'
// 这样是引入 b.js 中暴露出的常量 b
// 引入非default的部分时，引入名称需要与变量名称一致
//     import { c } from './b.js' ❌

console.log(a.name) // => 'aaa'
console.log(b.name) // => 'bbb'
```

### webpack [（中文文档）](https://webpack.docschina.org/concepts/)

webpack是一个打包工具。
模块化的代码无法被浏览器直接识别，需要通过 webpack 转义打包。

### Promise [（MDN 文档）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
`Promise` 是ES6中JS[回调地狱（Callback Hell）](https://zhuanlan.zhihu.com/p/39580112)的一种解决方案。

- new Promise()
```javaScript
// Promise 的构造函数接收一个回调函数作为其参数。该回调
// 函数有两个参数，resolve 成功时的回调；reject 失败时
// 候的回调。

// 定时器三秒后执行回调
const promise = new Promise(function (resolve, reject) {
    setTimeout(function () {
        // 随机成功失败
        if (Math.random() < 0.5) {
            resolve('data')
        } else {
            reject('reason')
        }
    }, 3000)
})
```
- then
```javaScript
// then
// 参数 resolveCallback 成功回调
// 参数 resolveCallback 失败回调
// 返回值 一个新的 promise 实例对象
promise.then(
    function (data) {
        console.log(data) // => 'data'
    },
    function (reason) {
        console.log(reason) // => 'reason'
    }
)
```
- catch
```javaScript
// then
// 参数 resolveCallback 失败回调 （ promise有异常抛出时也会被捕获 ）
// 返回值 一个新的 promise 实例对象
promise.catch(function (error) {
    // do something
})
```
链式调用
```javaScript
// 因为返回的都是promise对象、所以可以被链式调用
promise.then(function () { /* do something */ })
    .then(function () { /* do something */ })
    .then(function () { /* do something */ })
    .then(function () { /* do something */ })
    .catch(function () {})
```
项目中接口请求一般会被包装成一个返回promise对象函数，可以这样写
```javaScript
// 假设 getUserList 是一个api

const params = {
    lastName: 'Liu',
    age: 18,
    sex: SEX_MALE
}

getUserList(params)
    .then(function (userList){
        // todo
    })
    .catch(function (error) {
        alert('REQUEST FAILED')
    })
```

下面我们正式开始 [下一页](./vue.md)