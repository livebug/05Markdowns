

## 基础（自学）
### 安装

```bash
# npm install typescript -g 或者
# npm install typescript --save-dev
# tsc -v
Version 4.9.5
```

### 初始化 `tsconfig` 

```bash
tsc --init 
{
    "compilerOptions": {
        /* Projects */
        /* Language and Environment */
        "target": "es2016", /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
        /* Modules */
        "module": "commonjs", /* Specify what module code is generated. */
        "rootDir": "./src", /* Specify the root folder within your source files. */
        /* JavaScript Support */
        /* Emit */
        "declaration": true, /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
        "outDir": "./dist", /* Specify an output folder for all emitted files. */
        /* Interop Constraints */
        "esModuleInterop": true, /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
        "forceConsistentCasingInFileNames": true, /* Ensure that casing is correct in imports. */
        /* Type Checking */
        "strict": true, /* Enable all strict type-checking options. */
        /* Completeness */
        "skipLibCheck": true /* Skip type checking all .d.ts files. */
    }
}  
```

### 初始化  `package.json` 

```bash
npm init -y

npm install --save-dev typescript
npm install --save-dev ts-node @types/node
npm install --save-dev @types/node
```

### d.ts 文件是什么？

> d.ts就是TypedDefinition 类型定义文件，用来定义类型信息以及接口规范。

### @types/node 是什么

> 1.  本地安装node.d.ts。这是对Node.js的内置核心模块的TypeScript类型定义。理解为头文件好了。有了它可以让Intellisence提供代码补全功能。在终端里执行以下命令来安装。

```bash
npm install @types/node --save-dev
```

### npx 是什么？

> npx 是 npm5.2.0版本新增的一个工具包，定义为npm包的执行者，相比 npm，npx 会自动安装依赖包并执行某个命令。

### ts 项目的基础模板？

    |-- dist
    |   |-- index.d.ts
    |   -- index.js
    |-- node_modules
    |   |-- ... 
    |-- package-lock.json
    |-- package.json
    |-- src
    |   -- index.ts
    -- tsconfig.json

### ts的测试框架 jest 
还不是很会用
*   安装

    ```bash
    npm install -D jest ts-jest @types/jest
    npm install --save-dev jest typescript ts-jest @types/jest
    npm install --save-dev babel-jest @babel/core @babel/preset-env
    npm install --save-dev @babel/preset-typescript

    npm install --save-dev jest ts-jest @types/jest babel-jest @babel/core @babel/preset-env
    ```
*   配置 jest `jest.config.js`

    ```javascript
    // jest.config.js
    /** @type {import('ts-jest').JestConfigWithTsJest} */
    module.exports = {
      preset: 'ts-jest',
      testEnvironment: 'node',
    };
    ```
*   配置babel `babel.config.js` 

    ```javascript
    // babel.config.js
    module.exports = {
        presets: [
          ['@babel/preset-env', {targets: {node: 'current'}}],
          '@babel/preset-typescript',
        ],
      };
      
    ```

## TypeScript打包（教程文档）

### webpack整合

通常情况下，实际开发中我们都需要使用构建工具对代码进行打包；

TS同样也可以结合构建工具一起使用，下边以webpack为例介绍一下如何结合构建工具使用TS；

步骤如下：

#### 初始化项目

进入项目根目录，执行命令 ` npm init -y`，创建package.json文件

#### 下载构建工具

命令如下：

`npm i -D webpack webpack-cli webpack-dev-server typescript ts-loader clean-webpack-plugin`

共安装了7个包:

*   webpack：构建工具webpack
*   webpack-cli：webpack的命令行工具
*   webpack-dev-server：webpack的开发服务器
*   typescript：ts编译器
*   ts-loader：ts加载器，用于在webpack中编译ts文件
*   html-webpack-plugin：webpack中html插件，用来自动创建html文件
*   clean-webpack-plugin：webpack中的清除插件，每次构建都会先清除目录

#### 配置webpack

根目录下创建webpack的配置文件`webpack.config.js`：

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

module.exports = {
   optimization:{
       minimize: false // 关闭代码压缩，可选
   },

   entry: "./src/index.ts",

   devtool: "inline-source-map",

   devServer: {
       contentBase: './dist'
   },

   output: {
       path: path.resolve(__dirname, "dist"),
       filename: "bundle.js",
       environment: {
           arrowFunction: false // 关闭webpack的箭头函数，可选
       }
   },

   resolve: {
       extensions: [".ts", ".js"]
   },

   module: {
       rules: [
           {
               test: /\.ts$/,
               use: {
                   loader: "ts-loader"     
               },
               exclude: /node_modules/
           }
       ]
   },

   plugins: [
       new CleanWebpackPlugin(),
       new HtmlWebpackPlugin({
           title:'TS测试'
       }),
   ]
}
```

#### 配置TS编译选项

根目录下创建tsconfig.json，配置可以根据自己需要

```json
{
   "compilerOptions": {
       "target": "ES2015",
       "module": "ES2015",
       "strict": true
   }
}
```

#### 修改package.json配置

修改package.json添加如下配置

```json
{
   ...
   "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1",
       "build": "webpack",
       "start": "webpack serve --open chrome.exe"
   },
   ...
}
```

#### 项目使用

在src下创建ts文件，并在并命令行执行`npm run build`对代码进行编译；

或者执行`npm start`来启动开发服务器；

<br />

### Babel

除了webpack，开发中还经常需要结合babel来对代码进行转换；

以使其可以兼容到更多的浏览器，在上述步骤的基础上，通过以下步骤再将babel引入到项目中；

> 虽然TS在编译时也支持代码转换，但是只支持简单的代码转换；
>
> 对于例如：Promise等ES6特性，TS无法直接转换，这时还要用到babel来做转换；

安装依赖包：

`npm i -D @babel/core @babel/preset-env babel-loader core-js`

共安装了4个包，分别是：

*   @babel/core：babel的核心工具

*   @babel/preset-env：babel的预定义环境

*   @babel-loader：babel在webpack中的加载器

*   core-js：core-js用来使老版本的浏览器支持新版ES语法

修改webpack.config.js配置文件

```javascript
...
module: {
    rules: [
        {
            test: /\.ts$/,
            use: [
                {
                    loader: "babel-loader",
                    options:{
                        presets: [
                            [
                                "@babel/preset-env",
                                {
                                    "targets":{
                                        "chrome": "58",
                                        "ie": "11"
                                    },
                                    "corejs":"3",
                                    "useBuiltIns": "usage"
                                }
                            ]
                        ]
                    }
                },
                {
                    loader: "ts-loader",

                }
            ],
            exclude: /node_modules/
        }
    ]
}
...
```

如此一来，使用ts编译后的文件将会再次被babel处理；

使得代码可以在大部分浏览器中直接使用；

同时可以在配置选项的targets中指定要兼容的浏览器版本；


## 不要调整 package.json 的type 为module 
如果调整需要将所有的js文件判断为esm模块，会导致各种相关开发插件报错