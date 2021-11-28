### webpack的大概流程

#### 核心概念
- **Entry**：入口，Webpack 执行构建的第一步将从 Entry 开始，可抽象成输入。
- **Module**：模块，在 Webpack 里一切皆模块，一个模块对应着一个文件。Webpack 会从配置的 Entry 开始递归找出所有依赖的模块。
- **Chunk**：代码块，一个 Chunk 由多个模块组合而成，用于代码合并与分割。
- **Loader**：模块转换器，用于把模块原内容按照需求转换成新内容。
- **Plugin**：扩展插件，在 Webpack 构建流程中的特定时机注入扩展逻辑来改变构建结果或做你想要的事情。
- **Output**：输出结果，在 Webpack 经过一系列处理并得出最终想要的代码后输出结果。

#### 流程概括
- 初始化：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数；初始化 Compiler 对象，加载所有配置的插件
- 确定入口：根据配置中的 entry 找出所有的入口文件
- 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行编译，再找出该模块依赖的模块，递归完成依赖编译，生成编译后内容和依赖关系
- 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。

#### Loader
- loader是一个普通函数，默认参数时string字符串
- 同步返回
  ```javascript
  // 第一种
  return string
  // 第二种
  // 通过 this.callback 告诉 Webpack 返回的结果
  this.callback(null, source, sourceMaps);
  // 当你使用 this.callback 返回内容时，该 Loader 必须返回 undefined，
  // 以让 Webpack 知道该 Loader 返回的结果在 this.callback 中，而不是 return 中
  return
  ```
- 异步返回
  ```javascript
  // 告诉 Webpack 本次转换是异步的，Loader 会在 callback 中回调结果
  const callback = this.async();
  ```
- 声明需要二进制文件
  ```javascript
  module.exports = function(source) {
    // 在 exports.raw === true 时，Webpack 传给 Loader 的 source 是 Buffer 类型的
    source instanceof Buffer === true;
    // Loader 返回的类型也可以是 Buffer 类型的
    // 在 exports.raw !== true 时，Loader 也可以返回 Buffer 类型的结果
    return source;
  };
  // 通过 exports.raw 属性告诉 Webpack 该 Loader 是否需要二进制数据 
  module.exports.raw = true;
  ```
