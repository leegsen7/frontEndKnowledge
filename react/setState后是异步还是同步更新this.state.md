### setState后是异步还是同步更新this.state

---
1、`concurrent` 模式下都为异步

2、在 `legacy` 模式下：

React控制的事件处理程序，以及生命周期函数调用 `setState` 不会同步更新state。

React控制之外的事件中调用 `setState` 是同步更新的。比如原生js绑定 `addEventListener` 的事件，`setTimeout/setInterval` 等。

```javascript
class Case extends React.Component {
  componentDidMount() {
    // js原生绑定
    document.getElementById('btn').addEventListener('clcik', () => {
      this.setState({ count: this.state.count + 1})
      console.log(this.state.count)
    })
  }
}

setTimeout(() => {
  this.setState({ count: this.state.count + 1})
  console.log(this.state.count)
}, 10) 
```

[同步更新的源码和注释](https://github.com/facebook/react/blob/v17.0.2/packages/react-reconciler/src/ReactFiberWorkLoop.new.js#L593)

```javascript
// Flush the synchronous work now, unless we're already working or inside
// a batch. This is intentionally inside scheduleUpdateOnFiber instead of
// scheduleCallbackForFiber to preserve the ability to schedule a callback
// without immediately flushing it. We only do this for user-initiated
// updates, to preserve historical behavior of legacy mode.
// 现在刷新同步工作，除非我们已经在工作或在批处理中。
// 这是故意在scheduleUpdateOnFiber中而不是
// scheduleCallbackForFiber保留调度回调的能力
// 不需要立即冲洗.
// 我们只对用户发起的更新这样做，以保存遗留模式的历史行为。
```
