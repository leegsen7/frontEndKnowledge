## react新旧架构及其对比

### react理念
> React 用于构建**快速响应**用户界面的 `JavaScript` 库

### 两大瓶颈
- CPU瓶颈
  - 场景：当遇到大计算量的操作或者设备性能不足使页面掉帧，导致卡顿
  - 解决：时间分片渲染，将**同步的更新**变为可中断的**异步更新**
- IO瓶颈
  - 场景：发送网络请求后，由于需要等待数据返回才能进一步操作导致不能快速响应。
  - 解决：新增的`Suspense` 功能

### React15架构
- Reconciler（协调器）
  - 调用函数组件、或class组件的render方法，将返回的JSX转化为虚拟DOM
  - virtual dom diff
  - 通知**Renderer**将变化的虚拟DOM渲染到页面上
- Renderer（渲染器）
  - Renderer接到Reconciler通知，将变化的组件渲染在当前宿主环境
  - 浏览器渲染-ReactDOM
  - 移动端原生渲染-ReactNative

### React16架构
- Scheduler（调度器）
  - 调度任务的优先级，高优任务优先进入Reconciler
  - 原生api `requestIdleCallback`
- Reconciler（协调器）-render阶段（调用render方法获取virtual dom）
  - fiber架构
  - 时间分片
- Renderer（渲染器）-commit阶段（根据信息做提交渲染的动作）
