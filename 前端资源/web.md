### 1、关于CSS浮动的一些理解  
https://blog.csdn.net/qq_36595013/article/details/81810219
### 2、vue.config.js配置别名
const path = require('path')
const resolve = dir => path.join(__dirname, dir)
module.exports = {
  chainWebpack: (config) => {
    config.resolve.alias
      .set('@', resolve('src'))
      .set('assets', resolve('src/assets'))
      .set('api', resolve('src/api'))
      .set('views', resolve('src/views'))
      .set('components', resolve('src/components'))
  }
}
