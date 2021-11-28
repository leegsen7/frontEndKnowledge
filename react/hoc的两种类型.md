### hoc的两种类型
> 高阶组件（HOC）是 React 中用于复用组件逻辑的一种高级技巧。HOC 自身不是 React API 的一部分，它是一种基于 React 的组合特性而形成的设计模式。

#### 属性代理
通过对被包裹组件的props进行修改，或者添加新的props再传递给此组件
```javascript
const funcHoc = Component => {
  return class extends React.Component {
    render() {
      return (
        <Component
          {...this.props}
          {...otherProps}
        /> 
      )
    }
  }
}
```

#### 反向继承
继承入参类而不是React.Component，可通过super关键字获取到入参类的相关信息
```javascript
const iiHoc = Component => {
  // 注意继承的对象
  return class extends Component {
    render() {
      return super.render();
    }
  }
}
// 可通过super关键字为父类提供一个类生命周期方法
```
