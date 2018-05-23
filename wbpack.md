# webpack 
## 1.webpack是什么

- webpack  是现代 JavaScript 应用程序的静态模块打包器。
  	当 webpack 处理应用程序时，它会递归地构建一个依赖关系图，其中包含应用程序需要的每个模块，然后将所有这些模块从入口js开始打包，打包生成一个或多个 bundle。	
  * webpack 配置文件
          *  入口(entry)
          *  输出(output)
          *  loader
          *  插件(plugins)
## 2.下载webpack
  * npm install webpack -g   //全局下载webpack
  * npm install webpack --save-dev  //下载webpack为开发依赖
  
## 3. webpack模块化打包的基本流程(非常重要)
	
    	1> 连接: webpack从入口JS开始, 递归查找出所有相关联的模块, 并`连接`起来形成一个图(网)的结构
        2> 编译: 将JS模块中的模块化语法`编译`为浏览器可以直接运行的模块语法(当然其它类型资源也会处理)
		3> 合并: 将图中所有编译过的模块`合并`成一个或少量几个bundle文件, 而浏览器运行是打包生成的bundle文件 
## 4.webpack的基本配置和命令
        1> 默认配置文件为: webpack.config.js
            module.exports = {
              entry: '入口js',
              output: {
                filename: '打包生成的bundle'
              }
            }
        2> 打包命令
            webpack

###
	方式二: 纯命令实现模块化打包
			webpack app.js bundle.js  