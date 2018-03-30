webpack 4 配置
===============
为react使用的配置
------------------
create-react-app 的脚手架虽然实用，但是也有一些可能不符合需求的地方，如果使用eject弹出，由于webpack的配置非常复杂，不便于更改，所以自发配置是一件必要的事情
     

### 配置

#### 特点
webpack4的生产环境和开发环境是规定的

     webpack --mode development 开发环境  有注释等 
     webpack --mode production  生产环境  自带uglifyjs插件

   而且有些插件已经废弃，有些接口已经更改


总的来说，不需要以下插件
* ExtractTextWebpackPlugin 插件
* UglifyjsWebpackPlugin 插件
* 公共配置文件
* 生产环境配置文件
* 开发环境配置文件
* devServer配置
* NamedModulesPlugin插件
* NoEmitOnErrorsPlugin插件
* ModuleConcatenationPlugin插件
* CommonsChunkPlugin插件

提取公共库可用与rules同级的__optimizations__中plitChunks字段配置<br/>
__NoEmitOnErrorsPlugin__用optimization中__noEmitOnErrors__配置<br/>
__ModuleConcatenationPlugin__用optimization中__concatenateModules__配置<br/>
__NamedModulesPlugin__用optimization中__namedModules__配置<br/>
以上是比较常见的功能呢个，__ExtractTextWebpackPlugin__暂时找不到替代品
<br/><br/>module的写法已经更改，现按照官网的写法.出口和入口已经指定，但仍然可以手动配置自己定义的出入口，比如babel-polyfill等的应用，对于有其他需求的任然可以另起文件，最后在webpack-config.js中merge
### 提醒
为方便起见在此说明安装依赖
* webpack安装依赖 

      yarn add -D webpack@4.0.0 webpack-cli webpack-dev-server
* 模块安装依赖 ---当依赖增多时为查看方便，建议同意安装到生产环境 -D
* babel和react相关依赖

      yarn add -D babel-core babel-loader babel-plugin-import babel-plugin-transform-es2015-classes babel-plugin-transform-runtime babel-preset-es2015 babel-preset-react babel-preset-stage-0 babel-runtime 
为便于管理，建议新建.babelrc配置
* eslint相关依赖 

      yarn add -D eslint eslint-plugin-babel eslint-plugin-react 
还有相关插件，自行搜索 新建.eslintrc配置语法规则 新建.eslintignore 配置忽略模块
* postcss.config.js 由于postcss需新建一个文件配置解析，编译等功能，单独提一下，
       
     yarn add -D precss postcss-scss autoprefixer
依赖完成，对于相关文件的配置请自行浏览官网和搜索相关配置自行组合
* Documention 根据注释生成文档
      
    yarn add -D documentation

### 结语
最后在package.json修改命令配置


      "doc": "./node_modules/.bin/documentation build src/app.js -f md > API.md",
*****

      "lint": "eslint --cache --fix src",
*****

      "start": "yarn run lint && yarn run doc && webpack-dev-server --mode development --watch",
*****

      "build": " yarn run lint && yarn run doc && webpack --mode production",
注意命令的组成结构在测试期间可以更改缩短等待时间

##### 使用指南

     git clone git@github.com:jeoke/webpack4_react_eslint.git
   yarn install  或者 npm install