### 设置key的作用

---
`key` 是 `React` 用于追踪哪些元素被修改、被添加或者被移除的辅助标识。

在开发过程中，我们需要保证某个元素的 `key` 在其同级元素中具有唯一性。
在 `React Diff` 算法中 `React` 会借助元素的 `key` 值来判断该元素是新创建的还是被移动而来的元素，从而减少不必要的元素重复渲染。
