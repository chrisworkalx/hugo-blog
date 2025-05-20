+++
date = '2025-05-20T10:43:50+08:00'
draft = false
title = 'Webpack'
comments = true
author = "chrisworkalx"
tags =  ["Js","Webpack"]
categories =  ["高级"]
description =  "webpack详解"
slug = "webpack"
featured = true
+++

## Webpack 详解

### 1. Webpack 是什么

Webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 Webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将这些模块打包成一个或多个 bundle。

### 2. Webpack 的安装

```bash
npm install webpack webpack-cli --save-dev
```

### 3. Webpack 的配置

#### 3.1 entry

入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

```js
// webpack.config.js
module.exports = {
  entry: "./src/index.js",
};
```

#### 3.2 output

output 属性告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist/main.js。

```js
// webpack.config.js
module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: __dirname + "/dist",
  },
};
```

#### 3.3 loader

loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块。

```js
// webpack.config.js
module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: __dirname + "/dist",
  },
  module: {
    rules: [{ test: /\.css$/, use: "css-loader" }],
  },
};
```

#### 3.4 plugins

插件(plugins)用于执行范围更广的任务。插件可以用于 bundle 文件的优化，资源管理和环境变量注入。作用于整个构建过程。

```js
// webpack.config.js
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: __dirname + "/dist",
  },
  module: {
    rules: [{ test: /\.css$/, use: "css-loader" }],
  },
  plugins: [new HtmlWebpackPlugin({ template: "./src/index.html" })],
};
```

#### 3.5 mode

mode 用于指定当前的构建环境是：production、development 还是 none。设置 mode 可以启用 webpack 内置在相应环境下的优化。默认值为 production。

```js
// webpack.config.js
module.exports = {
  mode: "production",
};
```

### 4. Webpack 的构建流程

1. 初始化参数：从配置文件和 shell 语句中读取与合并参数，得出最终的参数；
2. 开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译；
3. 确定入口：根据配置中的 entry 找出所有的入口文件；
4. 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行编译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理；
5. 完成模块编译：在经过第 4 步使用 Loader 编译完所有模块后，得到每个模块被编译后的最终内容以及它们之间的依赖关系；
6. 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会；
7. 输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。
8. 在以上过程中，Webpack 会在特定的时间点广播出特定的事件，插件在监听到感兴趣的事件后会执行特定的逻辑，并且插件可以调用 Webpack 提供的 API 改变 Webpack 的运行结果。

### 5. Webpack 的优化

#### 5.1 代码分割

代码分割（Code Splitting）是 webpack 中最引人注目的特性之一。此特性能够把代码分离到不同的 bundle 中，然后可以按需加载或并行加载这些文件。代码分割可以用于获取更小的 bundle，以及控制资源加载优先级，如果使用合理，会极大影响加载时间。

#### 5.2 Tree Shaking

Tree Shaking 是一个术语，通常用于描述移除 JavaScript 上下文中的未引用代码(dead-code)。它依赖于 ES6 模块系统中的静态结构特性，例如 import 和 export。

#### 5.3 Scope Hoisting

Scope Hoisting 是 webpack3 中新增的功能，旨在通过分析模块间的依赖关系，尽可能的把打散的模块合并到一个函数中去，但前提是不能造成代码冗余。因此只有那些被引用了一次的模块才能被合并。

#### 5.4 代码压缩

代码压缩是 webpack 3 中新增的一个功能，它提供了 UglifyJSPlugin 插件，我们可以使用这个插件对代码进行压缩，从而减小包的大小，加快加载速度。

#### 5.5 使用 CDN 加速

#### 5.6 使用 SplitChunksPlugin 进行公共脚本分离

#### 5.7 使用 DllPlugin 预编译资源模块

#### 5.8 使用 externals 排除第三方库打包

#### 5.9 使用 HMR 提升开发效率

#### 5.10 使用 Tree Shaking 摇掉无用代码

#### 5.11 使用 Scope Hoisting 减少代码体积

#### 5.12 使用代码分割

#### 5.13 使用图片压缩

#### 5.14 使用动态 Polyfill

#### 5.15 使用 PWA 提升首屏加载速度

#### 5.16 使用 WebpackDevServer 提升开发效率

#### 5.17 使用 Webpack Analyzer 可视化 Webpack 项目结构和包体积

#### 5.18 使用 Webpack Bundle Analyzer 可视化 Webpack 项目结构和包体积

#### 5.19 使用 Webpack Dashboard 提升开发效率

### webpack4 编译构架流程

        +-------------------+
        | webpack(options)  |
        +--------+----------+
                 |
          创建 Compiler 对象
                 |
       调用 compiler.run()（或 watch）
                 |
        +--------v---------+
        | 初始化钩子: run   |
        +--------+---------+
                 |
     +-----------v------------+
     | 创建 Compilation 对象   |
     +-----------+------------+
                 |
         +-------v--------+
         | 解析 Entry     |
         +-------+--------+
                 |
      +----------v----------+
      | 构建模块（递归解析）|
      +----------+----------+
                 |
      +----------v----------+
      | 模块转化/加载/解析  |
      +----------+----------+
                 |
      +----------v----------+
      | Seal 优化阶段       |
      +----------+----------+
                 |
      +----------v----------+
      | 生成 Chunk & Asset  |
      +----------+----------+
                 |
      +----------v----------+
      | emit 写入输出目录   |
      +----------+----------+
                 |
      +----------v----------+
      | done 编译完成       |
      +---------------------+

#### 1. webpack(options)：初始化阶段

> 读取配置、创建 Compiler 实例。
> 初始化插件、注册各种 Hook（例如 run, emit, done 等）。

```js
const compiler = webpack(config);
```

#### 2. compiler.run()：编译阶段

> 调用 compiler.hooks.run。
> 可用于 CLI 插件、缓存准备等。

```js
compiler.hooks.run.tap("MyPlugin", (compiler) => {
  console.log("开始编译...");
});
```

#### 3. 创建 Compilation

> 调用 compiler.hooks.beforeCompile, compile, thisCompilation, compilation。
> Compilation 表示一次完整的构建任务，持有模块、资源等上下文

```js
compiler.hooks.thisCompilation.tap("MyPlugin", (compilation) => {
  // 可以操作模块、资源
});
```

#### 4. 构建模块（递归构建依赖图）

> 入口解析：调用 compilation.addEntry。

> 递归依赖构建模块树。

> 每个模块解析会触发：

- buildModule

- normalModuleLoader

- succeedModule

```js
compilation.hooks.buildModule.tap("MyPlugin", (module) => {
  console.log("构建模块：", module.resource);
});
```

#### 5. 优化阶段（seal）

> 执行模块优化、Chunk 优化、资源优化。
> Hook：optimize, optimizeModules, optimizeChunks, afterOptimizeAssets 等。

```js
compilation.hooks.optimizeAssets.tap("MyPlugin", (assets) => {
  // 修改输出资源
});
```

#### 6. 输出资源（emit）

> 调用 compiler.hooks.emit。

> 最终生成 dist 文件、目录等。

> 插件在这里最后修改资源文件内容。

```js
compiler.hooks.emit.tapAsync("MyPlugin", (compilation, callback) => {
  // 修改 asset 内容
  callback();
});
```

#### 7. 编译完成

> compiler.hooks.done。

> 输出日志、构建统计、通知等。

```js
compiler.hooks.done.tap("MyPlugin", (stats) => {
  console.log("构建完成", stats.toString());
});
```

### Webpack 4 构建核心对象关系

Compiler：Webpack 实例，全局唯一，生命周期范围大。

Compilation：每次构建都会新建一个，持有当前构建的模块、资源、chunk。

Module：每个依赖的模块（.js, .vue, .css）。

Chunk：一组模块打包的集合，通常对应一个入口。

Asset：最终生成的静态资源文件，如 main.js, style.css。

### 开发插件时的常用钩子一览（Webpack 4）

| 钩子                               | 类型  | 说明                       |
| ---------------------------------- | ----- | -------------------------- |
| `compiler.hooks.run`               | Sync  | 启动构建                   |
| `compiler.hooks.emit`              | Async | 资源输出前，修改最终内容   |
| `compiler.hooks.done`              | Sync  | 构建完成                   |
| `compilation.hooks.buildModule`    | Sync  | 每个模块构建时触发         |
| `compilation.hooks.optimizeAssets` | Async | 优化资源，如压缩或注释删除 |
| `compiler.hooks.watchRun`          | Async | Watch 模式重新构建前触发   |

### 实现一个 webpack4 所有生命周期钩子的插件

```js
// MyWebpackPlugin.js
class MyWebpackPlugin {
  constructor(options = {}) {
    this.options = options;
  }

  apply(compiler) {
    /** ========== 1. 构建启动 ========== */
    compiler.hooks.run.tap("MyWebpackPlugin", (compiler) => {
      console.log("[MyPlugin] 开始构建...");
      // 可以做缓存预热、日志初始化等
    });

    /** ========== 2. Watch 模式下文件变更 ========== */
    compiler.hooks.watchRun.tapAsync(
      "MyWebpackPlugin",
      (compiler, callback) => {
        console.log("[MyPlugin] watch 文件变更触发...");
        callback();
      }
    );

    /** ========== 3. 创建 compilation 对象 ========== */
    compiler.hooks.thisCompilation.tap("MyWebpackPlugin", (compilation) => {
      console.log("[MyPlugin] 创建 Compilation 实例");

      /** 3.1 每个模块开始构建时触发 */
      compilation.hooks.buildModule.tap("MyWebpackPlugin", (module) => {
        // 可以读取 module.resource，对指定模块做标记
        if (module.resource && module.resource.endsWith(".js")) {
          console.log(`[MyPlugin] 正在构建模块：${module.resource}`);
        }
      });

      /** 3.2 资源优化阶段，可用于修改构建结果 */
      compilation.hooks.optimizeAssets.tapAsync(
        "MyWebpackPlugin",
        (assets, callback) => {
          Object.keys(assets).forEach((filename) => {
            if (filename.endsWith(".js")) {
              let source = assets[filename].source();
              // 示例：去除 JS 文件中的注释（简单版本）
              const cleaned = source.replace(/\/\*[\s\S]*?\*\/|\/\/.*/g, "");
              assets[filename] = {
                source: () => cleaned,
                size: () => cleaned.length,
              };
              console.log(`[MyPlugin] 清理注释: ${filename}`);
            }
          });
          callback();
        }
      );
    });

    /** ========== 4. 输出阶段，可操作最终生成文件 ========== */
    compiler.hooks.emit.tapAsync("MyWebpackPlugin", (compilation, callback) => {
      console.log("[MyPlugin] emit 阶段 - 可以最终修改资源或注入额外内容");
      // 可以添加额外文件、清理无效资源、写入分析文件等
      callback();
    });

    /** ========== 5. 构建完成 ========== */
    compiler.hooks.done.tap("MyWebpackPlugin", (stats) => {
      console.log("[MyPlugin] 构建完成");
      // 可输出构建信息、构建时间、统计模块数量等
      console.log(
        stats.toString({
          colors: true,
          modules: false,
          entrypoints: false,
          chunks: false,
        })
      );
    });
  }
}

module.exports = MyWebpackPlugin;
```

### webpack5

Webpack 5 在构建流程上延续了 Webpack 4 的架构体系（仍基于 Tapable 的钩子机制），但在 资源处理、缓存、模块联邦、持久化存储 等方面进行了较大优化，尤其对生命周期钩子做了精细拆分。

下面详细介绍 Webpack 5 的 构建流程、与 Webpack 4 的主要区别，并给出每个阶段常用的钩子。

#### webpack5 构建流程图

```text
webpack(config)
|
创建 Compiler 实例
|
注册插件，初始化钩子
|
compiler.run()
|
compiler.hooks.beforeRun
|
compiler.hooks.run
|
创建 Compilation 实例
|
compilation.buildModule（递归依赖）
|
compilation.seal（模块优化、资源分组）
|
compilation.hooks.processAssets（多个阶段替代 emit）
|
compiler.hooks.done
```

#### webpack5 生命周期详解

| 】                   | 阶段                                        | 生命周期 Hook                                | 描述 |
| -------------------- | ------------------------------------------- | -------------------------------------------- | ---- |
| 初始化               | `beforeRun`、`run`                          | 执行构建前最后准备，比如检查配置、准备缓存等 |
| 创建 Compilation     | `thisCompilation`、`compilation`            | 每一次构建都会生成一个新的 Compilation       |
| 模块构建             | `compilation.hooks.buildModule`             | 每个模块构建开始时触发                       |
| 模块成功             | `succeedModule`                             | 模块构建成功后触发                           |
| 优化阶段             | `seal`, `optimizeModules`, `optimizeChunks` | 对模块/Chunk 进行 tree-shaking、合并等       |
| **资源处理（推荐）** | `compilation.hooks.processAssets`           | 替代 `emit` 的推荐方式，支持分阶段插入       |
| 构建完成             | `compiler.hooks.done`                       | 输出完资源后触发，可以输出日志、结果分析     |

#### Webpack 5 的资源处理阶段：processAssets

Webpack 5 推荐使用 compilation.hooks.processAssets 替代 Webpack 4 的 emit，它支持 多个阶段（stage），例如：

| Stage 常量                        | 描述                       |
| --------------------------------- | -------------------------- |
| `PROCESS_ASSETS_STAGE_ADDITIONAL` | 添加额外资源前             |
| `PROCESS_ASSETS_STAGE_DERIVED`    | 生成 source map 等派生资源 |
| `PROCESS_ASSETS_STAGE_OPTIMIZE`   | 优化资源（如压缩）         |
| `PROCESS_ASSETS_STAGE_SUMMARIZE`  | 生成打包摘要               |
| `PROCESS_ASSETS_STAGE_REPORT`     | 构建报告阶段（最晚）       |

##### 示例

```js
compilation.hooks.processAssets.tap(
  {
    name: "MyPlugin",
    stage: Compilation.PROCESS_ASSETS_STAGE_OPTIMIZE,
  },
  (assets) => {
    for (const filename in assets) {
      if (filename.endsWith(".js")) {
        const source = assets[filename].source();
        const transformed = source.replace(/console\.log\(.*?\);?/g, "");
        assets[filename] = new RawSource(transformed);
      }
    }
  }
);
```

#### webpack5 插件示例

```js
const { RawSource } = require("webpack-sources");

class ProcessAssetsStagePlugin {
  apply(compiler) {
    compiler.hooks.thisCompilation.tap(
      "ProcessAssetsStagePlugin",
      (compilation) => {
        const { Compilation } = compiler.webpack;

        /** 1. 添加额外资源前（ADDITIONAL） */
        compilation.hooks.processAssets.tap(
          {
            name: "ProcessAssetsStagePlugin",
            stage: Compilation.PROCESS_ASSETS_STAGE_ADDITIONAL,
          },
          (assets) => {
            compilation.emitAsset(
              "extra.txt",
              new RawSource("这是在 ADDITIONAL 阶段添加的文件")
            );
            console.log("[ADDITIONAL] 添加 extra.txt");
          }
        );

        /** 2. 生成派生资源（如 sourcemap）阶段（DERIVED） */
        compilation.hooks.processAssets.tap(
          {
            name: "ProcessAssetsStagePlugin",
            stage: Compilation.PROCESS_ASSETS_STAGE_DERIVED,
          },
          (assets) => {
            console.log(
              "[DERIVED] 可以在此阶段处理派生资源，例如生成自定义 sourcemap"
            );
          }
        );

        /** 3. 优化资源阶段（OPTIMIZE） */
        compilation.hooks.processAssets.tap(
          {
            name: "ProcessAssetsStagePlugin",
            stage: Compilation.PROCESS_ASSETS_STAGE_OPTIMIZE,
          },
          (assets) => {
            for (const filename in assets) {
              if (filename.endsWith(".js")) {
                const originalSource = assets[filename].source();
                const minified = originalSource.replace(
                  /console\.log\(.*?\);?/g,
                  ""
                );
                assets[filename] = new RawSource(minified);
                console.log(`[OPTIMIZE] 移除 console.log: ${filename}`);
              }
            }
          }
        );

        /** 4. 汇总构建结果阶段（SUMMARIZE） */
        compilation.hooks.processAssets.tap(
          {
            name: "ProcessAssetsStagePlugin",
            stage: Compilation.PROCESS_ASSETS_STAGE_SUMMARIZE,
          },
          (assets) => {
            const summary = Object.keys(assets)
              .map(
                (name) => `文件: ${name}, 大小: ${assets[name].size()} bytes`
              )
              .join("\n");

            compilation.emitAsset("summary.txt", new RawSource(summary));
            console.log("[SUMMARIZE] 生成构建文件摘要 summary.txt");
          }
        );

        /** 5. 报告阶段（REPORT） */
        compilation.hooks.processAssets.tap(
          {
            name: "ProcessAssetsStagePlugin",
            stage: Compilation.PROCESS_ASSETS_STAGE_REPORT,
          },
          () => {
            console.log("[REPORT] 构建资源处理完毕，可做最终日志或上报");
          }
        );
      }
    );
  }
}

module.exports = ProcessAssetsStagePlugin;
```

#### 如何使用这个插件

```js
const ProcessAssetsStagePlugin = require('./plugins/ProcessAssetsStagePlugin');

module.exports = {
  mode: 'production',
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: require('path').resolve(__dirname, 'dist'),
  },
  plugins: [
    new ProcessAssetsStagePlugin(),
  ],
};


# 构建后的效果说明：
# extra.txt：构建前添加的额外文件。

# main.js：在 OPTIMIZE 阶段清除了 console.log。

# summary.txt：构建文件体积汇总列表。

# 控制台日志：各阶段输出的构建信息。

```

### webpack5 和 webpack4 差异

| 特性              | Webpack 4              | Webpack 5                         | 差异说明                   |
| ----------------- | ---------------------- | --------------------------------- | -------------------------- |
| 文件输出          | `emit` 钩子统一处理    | 使用 `processAssets` 拆分多个阶段 | 更精细控制资源写入顺序     |
| 缓存系统          | 较弱（依赖插件）       | 内置持久化缓存（文件级别）        | 缓存可配置性强，构建速度快 |
| Module Federation | 不支持                 | 支持模块联邦（微前端）            | 大型项目拆分部署更方便     |
| 默认 polyfill     | 自动注入 Node 核心模块 | 不再自动引入（需手动处理）        | 更轻量、更现代的默认行为   |
| Target 兼容性     | 默认支持旧浏览器       | 更偏向现代平台（ES6+）            | 可配置 `target` 兼容性目标 |
