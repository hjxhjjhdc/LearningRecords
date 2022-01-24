# px2rem插件

> 因为设计师每次给的都是px的图，这里要自己计算转换rem很头疼，所以这里使用插件进行px与rem的转换

## rem的响应式设计

这里是我一个全局的js文件，根据设备的宽度和设计稿来动态的另一rem的大小，因此在项目中直接按照设计稿计算出对应的rem来写，设备就能自动适配



```bash
/* eslint-disable */
(function(doc, win) {
    var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function() {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;
            docEl.style.fontSize = 20 * (clientWidth / 375) + 'px';
        };
    if (!doc.addEventListener) return;
    win.addEventListener(resizeEvt, recalc, false);
    doc.addEventListener('DOMContentLoaded', recalc, false);
})(document, window);
// 这里在375的设备上1rem = 20px，在其他屏幕宽的时候会自动根据这个比例来动态调整
```

## 第一款： px2rem

> 这款插件是集成到项目中的，如果你的项目是使用vue-cli自动构建工具构件的，建议参考如下配置

1. 安装



```bash
npm install px2rem-loader
```

1. 配置
    webpack.base.conf.js > 在module> rules 下添加



```bash
{
    test: /\.scss$/,
    loaders: ["style", "css", "sass"]
}
```

3.找到utils.js这个文件 在cssloader 后面加入



```bash
var px2remLoader = {
    loader: 'px2rem-loader',
    options: {
      remUnit: 40 // 40px = 1rem
            remPrecision: 8 // rem的小数点后位数
    }
  }
再然后把这行替换成
  const loaders = options.usePostCSS ? [cssLoader, postcssLoader] : [cssLoader]
这个
  const loaders = [cssLoader, px2remLoader];
```

注意： 这里的流程中有两次转换第一次 css中的px转换为px2rem的rem，这里是 40px = 1rem，第二步是rem适配到页面 ，这里的rem与像素比是根据屏幕宽度动态计算的，以375的设备为例是 1rem = 20px转换到页面中显示.这样最终实现 输入 40px，屏幕上20px的效果，因为我UI标注是按照2倍图来的，所以直接按照标注写就自己转换了。

4.重启项目就可以了

## cssrem 插件

> 这个是vscode ide 的一款插件，主要实现了在书写代码的时候直接将px转成rem

1. vscode安装插件
    2.配置



```bash
参数配置文件：VSCode -> 文件 -> 设置 -> 搜索cssrem

cssrem.rootFontSize root font-size (unit: px), default: 16
cssrem.fixedDigits px转rem小数点最大长度，默认：6。
cssrem.autoRemovePrefixZero 自动移除0开头的前缀，默认：true
```

3.书写的时候就会有提示 ，可以直接转换rem

