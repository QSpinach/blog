### Webpack

#### 安装

本地安装

```bash
npm install --save-dev webpack
npm install --save-dev webpack@<version>
```

全局安装

```bash
npm install --gobal webpack
```

#### 基本使用

```js
const path = require('path');

module.exports = {
  entry: './src/index.js', // 入口文件
  output: { // 出口文件
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

资源管理

css加载，需安装css-loader和style-loader并在module配置

```bash
npm install --save-dev style-loader css-loader
```

```js
const path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
   module: {
     rules: [
       {
         test: /\.css$/,
         use: [
           'style-loader',
           'css-loader'
         ]
       }
     ]
   }
  };
```

less加载，需安装less-loader并在module配置,安装less-loader时需要安装less

```bash
npm install --save-dev less-loader less
```

```json
module: {
     rules: [
       {
         test: /\.less/,
         use: [
           'style-loader',
           'css-loader',
           'less-loader'
         ]
       }
     ]
   }
```

sass加载，需安装sass-loader并在module配置,安装sass-loader时需要安装node-sass

node-sass需要在淘宝镜像源下安装

```bash
npm install --save-dev sass-loader node-sass
```

```json
module: {
     rules: [
       {
         test: /\.scss/,
         use: [
           'style-loader',
           'css-loader',
           'sass-loader'
         ]
       }
     ]
   }
```

图片路径，需安装配置url-loader

```bash
npm install --save-dev url-loader
```

```json
module: {
  rules: [
    {
      test: /\.(png|svg|jpg|gif)$/,
      use: [{
        loader: 'url-loader',
        options: {
          limit: 2048,
          name: '[hash:8]-[name].[ext]'
        }
      }]
    }
  ]
}
```



图片加载，需安装配置file-loader

```bash
npm install --save-dev file-loader
```

```js
module: {
  rules: [
    {
      test: /\.(png|svg|jpg|gif)$/,
      use: [
        'file-loader'
      ]
    }
  ]
}
```

字体加载同样需要安装配置file-loader

```js
module: {
  rules: [
    {
      test: /\.(woff|woff2|eot|ttf|otf)$/,
      use: [
        'file-loader'
      ]
    }
  ]
}
```

加载数据,如 JSON 文件，CSV、TSV 和 XML。使用csv-loader和xml-loader安装配置即可处理CSV、TSV 和 XML类型的文件。

```bash
npm install --save-dev csv-loader xml-loader
```

```js
module: {
  rules: [
    {
      test: /\.(csv|tsv)$/,
      use: [
        'csv-loader'
      ]
    },
    {
      test: /\.xml$/,
      use: [
        'xml-loader'
      ]
    }
  ]
}
```

`HtmlWebpackPlugin` 创建了一个全新的文件，所有的 bundle 会自动添加到 html 中。

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: {
    app: './src/index.js',
    print: './src/print.js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, './src/index.html'),
      filename: 'index.html',
      title: 'Output Management'
    })
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
}

```

`HtmlWebpackPlugin` 在每次构建前清理 `/dist` 文件夹

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');

module.exports = {
  entry: {
    app: './src/index.js',
    print: './src/print.js'
  },
  plugins: [
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin({
      title: 'Output Management'
    })
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
}

```

为了更容易跟踪错误和警告JavaScript 提供了 `source map` 功能。

```js
module.exports = {
	devtool: 'inline-source-map',
}
```

`webpack-dev-server` 提供了一个简单的 web 服务器，并且能够实时重新加载(live reloading)。

```js
// webpack.js
module.exports = {
  devServer: {
    contentBase: './dist'
  },
}
```

```js
// package.json
"scripts": {
  "server": "webpack-dev-server --open"
}
```

模块热替换是webpack内置的功能，无需进行完全刷新。

```js
// webpack.js
module.exports = {
  devServer: {
    contentBase: './dist',
    hot: true
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ]
}
```

tree shaking移除 JavaScript 上下文中的未引用代码(dead-code)。从 webpack 4 开始，也可以通过 `"mode"` 配置选项轻松切换到压缩输出，只需设置为 `"production"`。

```js
module.exports = {
  mode: "production"
}
```

要让代码支持es6及更高语法需要以下步骤

```js
/** 
	1、安装第一套包 npm install babel-core babel-loader babel-plugin-transform-runtime --dev-save
	2、安装第二套包 npm install babel-preset-env babel-preset-stage-0 --save-dev
	3、webpack配置文件添加新的匹配规则 {test: /\.js$/, use: 'babel-loader', exclude: /node_modules/}
	4、根目录下新建.babelrc的Babel配置文件 {"presets": ["env", "stage-0"], "plugins": ["transform-runtime"]}
**/
```

修改包文件的入口和出口文件

```js
resolve: {
    // 自动补全的扩展名
    extensions: ['.js', '.vue', '.json'],
    // 默认路径代理
    // 例如 import Vue from 'vue'，会自动到 'vue/dist/vue.common.js'中寻找
    alias: { // 别名
        '@': path.resolve('src'),
        '@config': path.resolve('config'),
        'vue$': 'vue/dist/vue.common.js'
    }
}
```



#### 生产环境



#### 问题

WARNING in asset size limit: The following asset(s) exceed the recommended size limit (244 KiB).解决

在webpack中配置

```js
performance: {
	hints:false
}
```

webpack中如何使用vue

1. 安装vue包
2. 安装解析vue文件的vue-loader vue-template-complier
3. 在入口文件main.js中导入vue模块
4. 定义vue组件，组件组成部分template，script，style
5. 导入定义好的组件
6. 创建vue实例 new Vue({ el: '#app', render: c => c(login) })
7. 在页面中创建一个id为app的div元素，作为我们vue实例控制区域

vue中引入mui.min.js报错，解决办法在.babel中加入

```js
"ignore":[  './src/assets/js/mui.js']
```

