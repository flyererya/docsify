## rem

lib-flexible 会自动设置 html 的 font-size 为屏幕宽度除以 10，也就是 1rem 等于 html 根节点的 font-size。同时会在 body 标签上添加 font-size = 12px 的样式，所以不用担心整个 css 会继承 html 的 font-size 导致所有通过继承的字体小大变大。但是当分辨率大于 540px，它便不再生效。

```javascript
npm install lib-flexible --save-dev
npm i postcss-plugin-px2rem  --save -dev
```

1. 在 main.js 中引入 lib-flexible

```javascript
// main.js
import "lib-flexible";
```

2. 在 vue.config.js 中配置一下

```javascript
module.exports = {
    css: {
        loaderOptions: {
            css: {},
            postcss: {
                plugins: [
                    require("postcss-plugin-px2rem")({
                        rootValue: 198, //换算基数， 默认100
                    }),
                ],
            },
        },
    },
};
```

移动端的话一般是 750<br>
但是但是但是<br>
pc 端的大屏怎么办！！<br>

找到 flexible.js 文件,修改 540 那里就可以了，比如你公司的设计稿是 1980px 的，就设置成设计稿的大小

```javascript
function refreshRem() {
    var width = docEl.getBoundingClientRect().width;
    if (width / dpr > 1980) {
        width = 1980 * dpr;
    }
    var rem = width / 10;
    docEl.style.fontSize = rem + "px";
    flexible.rem = win.rem = rem;
}
```

> 需要注意的是：每次 npm 都要重新改一边，所以可以直接把 flexible.js 下载下来
