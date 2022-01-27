该方法主要用来做网站自适应的，同时可以实现撑起内容高度，避免图片加载后导致的页面滚动。

一、可以使用js判断图片的宽度得到具体数值之后，再来利用js设置图片的高度（这里就不具体为大家细说了）。

利用js来实现有一个缺点就是只能在页面刷新的时候才能调整图片的高度，不能随着浏览器的窗口大小变化来实现自适应。

二、我这次主要是用css来实现图片高度的自适应问题。

下面是所需要的代码

（这种方法是可以在图片上方垂直居中展示文字的，如果不需要可以选择最下方更简洁的代码）

<div class="box">
	<span>行内元素垂直居中</span>
	<div class="img-box">
		<img src="123.jpg"/>
        </div>
</div>

.box{
	width: 50%;
	margin: 50px auto;
}
.img-box{
	width: 100%;
	position:relative;
	z-index:1;
}
.img-box img{
	position:absolute;
	top:0;
	bottom:0;
	left:0;
	right:0;
	width:100%;
	margin:auto;
	z-index: -1;
	*zoom:1;
}
.img-box:before {
	content: "";
	display: inline-block;
	padding-bottom: 100%;
	width: 0.1px;	/*必须要有数值，否则无法把高度撑起来*/
	vertical-align: middle;
}


1、这里主要为大家说明的就是padding-bottom这个属性，当它的值为百分比的时候，是按该元素的宽度来计算的。所以当设为100%的时候，其高度就等于自身的宽度，形成一个正方形。当然，这个数值可以根据实际情再进行调整。
2、其次要说明的就是我们引用的图片是通过绝对定位来布局的，这样才能使图片跟随其父元素的大小改变来实现自适应。



另一种简洁的方法就是直接在img的父元素上加padding-bottom就行了

<div class="img-box">
	<img src="123.jpg"/>
</div>

.img-box{
	padding-bottom:100%;
}
.img-box img{
	position:absolute;
	top:0;
	bottom:0;
	left:0;
	right:0;
	width:100%;
	margin:auto;
