### virtual dom diff算法

前提：将前后两棵树完全比对的算法的复杂程度为 `O(n**3)`，其中n是树中元素的数量

优化限制：
1. 只对同级元素进行`Diff`
2. 两个不同类型的元素对比会直接销毁
3. 同级元素可以通过设置`key`，来追踪元素的修改、移动、添加、删除

#### 单节点diff
key和dom type一致才能复用

#### 多阶段diff
- 遍历newChildren和oldFiber
- 不可使用双指针，因为fiber数据是单链表形式存储的
- 更新操作的频率高：第一轮处理更新，第二轮处理非更新
- **第一轮遍历**：key相同继续遍历，对比出可复用的fiber（key相同但type不同，会将oldFiber标记为DELETION，继续遍历），key不同或有一方结束则跳出遍历
- **第二轮遍历**：
    - newChildren与oldFiber同时遍历完：diff结束
    - newChildren没遍历完，oldFiber遍历完：遍历剩下的newChildren新节点，生成fiber
    - newChildren遍历完，oldFiber没遍历完：遍历剩下的oldFiber，标记为DELETION
    - newChildren与oldFiber都没遍历完，下一步处理移动的节点
- 处理移动的节点
    - 将未遍历的oldFiber中的key生成map，可根据key和map找到可复用
    - 标记节点是否移动
    - 节点只会往后面移动，不会出现节点后面移动到前面的操作
