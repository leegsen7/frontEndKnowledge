### setState后是异步还是同步更新this.state

---
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
