## SVG Progress 渐变

https://www.zhangxinxu.com/wordpress/2015/07/svg-circle-loading/   张鑫旭

实际项目开发时候，设计师设计的还原可能不是下面这种纯色的圆环，而是一种复合渐变效果，类似下图：

![彩条圆环](https://image.zhangxinxu.com/image/blog/201711/2017-11-02_221910.png)

也是可以实现的，原理是使用两个渐变半圆无缝叠加在一起就可以了。

完整案例（含10秒倒计时JS代码），可狠狠地点击这里体验：[SVG与多彩渐变圆环倒计时效果demo](http://www.zhangxinxu.com/study/201710/colorful-time-count-down-svg-circle.html)

其中SVG中使用了3个`<circle>`，如下截图：
![3个圆环元素](https://image.zhangxinxu.com/image/blog/201711/2017-11-02_222519.png)

分别表示底部灰色完整圆环，左半渐变圆环和右半渐变圆环。

