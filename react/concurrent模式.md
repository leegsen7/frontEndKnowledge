## concurrent模式

- legacy 模式：当前的使用方式，`ReactDOM.render(<App />, rootNode)`
- blocking 模式：过度模式，`ReactDOM.createBlockingRoot(rootNode).render(<App />)`
- concurrent 模式：未来的模式，`ReactDOM.createRoot(rootNode).render(<App />)`

![./images/concurrent模式-1.png]

---
从源码层面讲，Concurrent Mode是一套可控的“多优先级更新架构”。
