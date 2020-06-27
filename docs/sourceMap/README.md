```javascript
const development = process.env.NODE_ENV !== "production";
module.exports = {
    configureWebpack: (config) => {
        //"cheap-source-map"转换过的源码-快
        // "source-map" 源码-慢
        // 开发环境配置
        if (development) {
            config.devtool = "source-map";
        }
    },
    css: {
        //查看CSS属于哪个css文件
        sourceMap: true,
    },
};
```
