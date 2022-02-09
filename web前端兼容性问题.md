## 一、Web前端兼容性问题

一直以来，Web前端领域最大的问题就是兼容性问题，没有之一。

 

前端兼容性问题分三类：

- 浏览器兼容性
- 屏幕分辨率兼容性
- 跨平台兼容性

 

### 1、浏览器兼容性问题

第一次浏览器大战发生在上个世纪90年代，微软发布了IE浏览器，和网景公司的Netscape Navigator大打出手，1998年网景不得不将公司卖给AOL。没有了对手的IE不思进取，W3C标准支持发展缓慢，为以后的IE兼容性灾难埋下了伏笔。到2004年，IE的市场份额达到95%，但在此之后IE的份额逐步遭其他浏览器蚕食，主要包括Firefox，Chrome，Safari和Opera。.

 

2001年8月27日，微软发布IE6，时隔五年直到2006年才发布了IE7。2009年3月19日，经历了众多测试版后，IE8最终发布，虽然IE8针对旧版IE在多方面做了很大改进，但在HTML5、CSS 3等标准支持方面仍落后于其他浏览器对手。这三个版本的IE是所有兼容性问题的最大根源，堪称前端噩梦。

 

IE6、7、8不支持HTML5、CSS3、SVG标准，可被判定为“极难兼容”

IE9不支持Flex、Web Socket、WebGL，可被判定为“较难兼容”

IE10部分支持Flex（-ms-flexbox）、Web Socket，可被判定为“较易兼容”

IE11部分支持Flex、WebGL，可被判定为“较易兼容”

 

IE6、7、8、9可视为“老式浏览器”

IE10、11可视为“准现代浏览器”

Chrome、Firefox、Safari、Opera 、Edge可视为“现代浏览器”

 

#### 浏览器与Windows版本份额

Statcounter的各项数据以2020年6月为基准。

http://gsa.statcounter.com/

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621222310428-1780413925.png)

 

 **2、屏幕分辨率兼容性问题**

在不同的屏幕分辨率，浏览器页面展示差异很大。特别是屏幕分辨率较小时，容易发生布局错乱。为了解决这个问题，响应式UI框架应运而生。

 

主流桌面屏幕分辨率宽度集中在1280~1920，高度集中在720~1080；

主流平板屏幕分辨率宽度集中在962~1280，高度集中在601~800。

主流移动屏幕分辨率宽度集中在360~414，高度集中在640~896。

 

典型的桌面屏幕分辨率：1920x1080

典型的便携屏幕分辨率：1366x768

典型的平板屏幕分辨率：768x1024

典型的移动屏幕分辨率：360x640

 

Bootstrap定义（参考系是逻辑分辨率）：

| 分辨率   | 设备名                | 典型屏幕                   |
| -------- | --------------------- | -------------------------- |
| >=1400px | xxl 超超大屏设备      | 桌面屏幕                   |
| >=1200px | xl 超大屏设备         | 便携屏幕                   |
| >=992px  | lg 大屏设备           | 竖屏桌面屏幕、横屏平板屏幕 |
| >=768px  | md 中屏设备           | 竖屏平板屏幕               |
| >=576px  | sm 小屏设备           | 横屏移动屏幕               |
| <576px   | xs 超小屏（自动）设备 | 竖屏移动屏幕               |

注：Bootstrap5新增xxl，Bootstrap3中的lg>=1200px，无576px档。

 

#### 手机屏幕分辨率说明

由于手机屏幕尺寸过小，使用原始分辨率会使得页面显示过小，因此使用了逻辑分辨率，用倍数放大的方法来保证兼容性。比如iOS app的UI资源区分@1x、@2x和@3x，这就是指原始分辨率对逻辑分辨率的倍数，被称为设备像素比DPR。所以大部分人的手机分辨率都是1080x1920，在分类中却被归为了360x640。这个分辨率和CSS中的PX是一致的。

 

#### 桌面屏幕分辨率说明

移动设备一开始就考虑了DPR，而Windwos桌面的分辨率由于历史原因却没有这一概念，于是Windwos引入了DPI，最初是设置DPI，后来是设置DPI比例。比如设置DPI比例=125%，你可以查询Chrome的window.devicePixelRatio，这时输出1.25，这说明DPI比例=DPR。但是大部分老程序并不支持DPI（Unaware），所以当你设置高DPI时，只能等比放大，字模糊到眼要瞎，最后落得空有大屏只能用超低分辨率。由于Chrome支持DPI，所以并不担心Web有DPI问题。但需要注意的是与手机屏幕分辨率不同，桌面分辨率要除以DPI比例，才是逻辑分辨率。如1920x1080设置DPI比例=1.25，逻辑分辨率实际为1536x864。

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621203756691-1581945714.png)

 

#### 屏幕分辨率基础概念说明

| 缩写 | 全称                       | 说明                                                         |
| ---- | -------------------------- | ------------------------------------------------------------ |
| PX   | Device Pixels              | 设备像素，指设备的物理像素                                   |
| PX   | CSS Pixels                 | CSS像素，指CSS样式代码中使用的逻辑像素                       |
| DOT  | Dot                        | 点，屏幕或打印纸上的点，等同物理像素                         |
| PT   | Point                      | 磅（传统长度单位）为1/72英寸=0.35mm                          |
| PT   | iOS Point                  | 磅（iOS长度单位），为1/163英寸，等同于CSS逻辑像素            |
| DP   | Density independent Pixels | 设备无关像素（Android长度单位），为1/160英寸，等同于CSS逻辑像素 |
| SP   | Scale independent Pixels   | 缩放无关像素（Android字体单位），等同于CSS逻辑像素，但文字尺寸可调（单独缩放） |
| DPR  | Device Pixel Ratio         | 设备像素比，指CSS逻辑像素对于物理像素的倍数                  |
| DPPX | Dots Per Pixel             | 等同于DPR                                                    |
| PPI  | Pixel Per Inch             | 屏幕上每英寸(2.54厘米)的像素点个数                           |
| DPI  | Dots Per Inch              | 屏幕或纸上每英寸(2.54厘米)的点个数，标准密度：传统打印=72；Windows=96；Android=160；iOS=163。 |
| DPIR | DPI Ratio                  | DPI缩放比例，指DPI对于Windows标准DPI的倍数=DPI/96，等同于DPR |

注：各厂商概念有重名现象，请注意区分。

 

#### 各平台屏幕分辨率份额

![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621221931066-1372582236.png)

 

**3、跨平台兼容性问题** 

随着移动和平板市场的日益发展，Web在桌面、平板、移动平台上的兼容性问题日益突出。由于移动和平板是触摸式操作，与桌面的鼠标操作方式有很大差异，因此在不同平台上要做相应修改。为了解决这个问题，诞生了跨平台框架，在不同平台上，外观、布局、操作都有差异化修改。

 

#### 各平台份额

![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621222506691-1624062390.png)

 

## 二、前端里程碑框架

在前端领域，随着技术的不断进步，逐步诞生了一些里程碑式的前端框架。这些前端框架，大致也是随着兼容性问题的发生、发展而诞生、发展的。

 

这些框架代表了前端应用当时先进、成熟、主流的开发方式与发展方向，兼容性问题也在这些框架的基础之上不断得到解决，大致也分为三个阶段：

一、DOM操作框架，代表框架：jQuery

二、响应式框架，代表框架：Bootstrap

三、前端MVC框架，代表框架：React、Angular、Vue

 

### 1、JQuery

2006年1月John Resig等人创建了jQuery；8月，jQuery的第一个稳定版本。jQuery是DOM操作时代前端框架最优秀，也几乎是唯一代表；但是在以React为代表的新式前端框架崛起之后，迅速没落。

 

- JQuery 1.x兼容IE6+浏览器
- JQuery 2.x兼容IE9+浏览器
- JQuery 3.x兼容IE9+浏览器

 

### 2、Bootstrap

Bootstrap原名Twitter Blueprint，由Mark Otto和Jacob Thornton开发，最经典的响应式CSS框架，在2011年8月19日作为开源项目发布。其核心是16列布局栅格系统，使用媒体查询设定阈值为超小屏幕，小屏幕，中等屏幕，大屏幕，超大屏幕创建不同的样式。

 

- Bootstrap 2兼容IE7+浏览器
- Bootstrap 3兼容IE8+浏览器
- Bootstrap 4兼容IE10+浏览器
- Bootstrap 5不兼容IE浏览器

 

### 3、React

React 起源于 Facebook 的内部项目，在前端MVC框架大潮中诞生并走红。2013年5月开源，凭借Virtual Dom，JSX，Flux，Native等一大批创新特性，迅速吸引了大量开发人员，至今仍是最先进的前端JS框架。

 

### 4、Angular

AngularJS 诞生于2009年，由Misko Hevery 等人创建，后为Google所收购。由于Google不差钱，所以AngularJS经历颠覆性升级为Angular。Angular最大的特点就是大而全。

 

### 5、Vue

2013年，在Google工作的尤雨溪，受到Angular的启发，从中提取自己所喜欢的部分，开发出了一款轻量框架，最初命名为Seed，后更名为Vue。

 

## 三、浏览器兼容框架

在前端发展的初期，大多数开发最关注的问题就是浏览器兼容问题，迫切需要兼容所有浏览器的JS和CSS框架。这阶段除了横空出世的jQuery，还有一些其它方面的兼容框架。

 

### 1、normalize.css

让不同的浏览器在渲染网页元素的时候形式更统一。

 

### 2、html5shiv.js

IE6~IE8识别HTML5标签，并且可以添加CSS样式。

 

### 3、respond.js

使IE6~IE8浏览器支持媒体查询。

 

## 四、响应式框架

有了jQuery等兼容框架的基础，开发人员的关注点，逐渐转移到越来越丰富的屏幕分辨率上，除开Bootstrap一家独大，越来越多的响应式框架也在奋起直追。

 

### 1、Semantic UI

https://github.com/semantic-org/semantic-ui

Semantic 是一个设计漂亮的响应式布局的语义化框架。

 

### 2、Bulma

https://github.com/jgthms/bulma

基于 Flexbox 的现代 CSS 框架

 

### 3、Tailwind

https://github.com/tailwindcss/tailwindcss

Tailwind是一个底层CSS 框架，快速 UI 开发的实用工具集，提供了高度可组合的应用程序类，可帮助开发者轻松构建复杂的用户界面。另外Tailwind + Styled Component 简直是绝配（摘自知乎https://www.zhihu.com/question/337939566）。

 

### 4、Materialize

https://github.com/Dogfalo/materialize

A CSS Framework based on Material Design.

 

### 5、Foundation

https://github.com/foundation/foundation-sites

The most advanced responsive front-end framework in the world.

 

### 6、Pure.css

https://github.com/pure-css/pure

A set of small, responsive CSS modules

 

### 7、YAMLCSS

https://github.com/yamlcss/yaml

YAML is a modular CSS framework for truly flexible, accessible and responsive websites.

 

兼容IE6+浏览器（能兼容IE6的太稀少了）

 

## 五、跨平台框架

自2009年以来，由于Node.js生态的不断发展，前端开发的势力大涨， AngularJS，BackboneJS，KnockoutJS等一批前端MVC框架开始出现。最终伴随着React、Angular、Vue等框架的脱颖而出，用前端框架开发移动、桌面应用的野心开始暴涨，开始关注不同平台的差异化，越来越多的跨平台框架开始出现。

 

### 1、Framework7

https://github.com/framework7io/framework7

Build iOS, Android & Desktop apps

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621203837907-1960426437.png)

 从上图可以看出，桌面版本比移动版本更紧凑，控件风格跟所在平台近似。支持三种主题：ios、 md、 aurora对应不同平台。

 

### 2、Ionic

https://github.com/ionic-team/ionic

build mobile and desktop apps

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621203906170-1588133102.png)

 从上图可以看出，主要针对移动平台优化，但通过API支持多种平台。

 

### 3、Onsen UI

https://github.com/OnsenUI/OnsenUI

develop HTML5 hybrid and mobile web apps

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621203922979-672184810.png)

 从上图可以看出，主要针对移动平台优化，但通过API支持多种平台。

 

### 4、Quasar Framework

https://github.com/quasarframework/quasar

基于Vue构建响应式网站、PWA、SSR、移动和桌面应用

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621203939278-1076609827.png)

 Quasar将一些辅助CSS类附加到document.body：如desktop、mobile、touch、platform-[ios]、within-iframe等


**5、UNI-APP** 

https://github.com/dcloudio/uni-app

使用 Vue.js 开发所有前端应用的框架

 ![img](https://img2020.cnblogs.com/blog/569097/202006/569097-20200621204001037-1975883272.png)

 从上图可以看出，三种平台比较一致，但移动版本还比桌面版本还紧凑是什么意思？

 

### 6、横向对比

| 框架       | 桌面优化 | 移动优化 | 移动一致 | 支持框架 |
| ---------- | -------- | -------- | -------- | -------- |
| Framework7 | 优秀     | 优秀     | 优秀     | 最多     |
| Ionic      | 一般     | 优秀     | 一般     | 较多     |
| Onsen UI   | 一般     | 优秀     | 一般     | 较多     |
| Quasar     | 良好     | 优秀     | 良好     | Vue      |
| UNI-APP    | 一般     | 优秀     | 优秀     | Vue      |

 

## 六、总结

兼容性问题总是伴随着平台的扩张而产生的，Web开发面临的终极问题就是多平台兼容性问题，根据不同产品，不同阶段做部分取舍，应用不同的框架而已。需要支持的平台，决定了你的选择。

 

新的框架或旧框架的新版本基本都不再支持IE，但国内还有5.65% 的IE用户，而且3.29%的WinXP，46.79%的Win7都是潜在的IE用户，所以可将其做为一个平台看待。

- IE Web
- Desktop Web
- Mobile Web
- Tablet Web
- Desktop Hybrid
- Mobile Hybrid
- Tablet Hybrid

注：React Native代表的Native技术不在本次讨论之列

 

### 1、浏览器兼容策略

国内XP用户还有3.29%，XP用户既升级不了IE9，也无法安装新版本Chrome和Firefox 。而IE用户还有 5.65%，考虑到Windows用户为87%，所以IE9+的份额应该要少于5.65%-3.29%*87%=2.79%。也就是说IE8以下的用户要多于IE8以上的用户。所以支持单独支持IE9+ 浏览器没有实际意义，要么支持IE6，要么不支持IE，。

 

看看知名网站对IE8的兼容性，

- 京东会提示“温馨提示：您当前的浏览器版本过低，存在安全风险，建议升级浏览器”，但是页面完全可以正确显示，几乎没有什么异常发生，看来兼容工作很到位。
- 淘宝会出现很多页面异常，说明IE兼容工作要求不高，基本正常即可，只是象征性的加了几条兼容性内容。
- 去哪儿网也会出现很多页面异常，但页面布局还是正常的，看来也是尽力而为，不做要求。
- 腾讯的页面只有一个立即更新按钮，一贯地友好。
- 知乎直接404，好吧，强大。

 

兼容IE的建议：

一、建议不做任何兼容，IE6~11直接显示升级浏览器按钮。

二、如果一定要兼容，后端返回IE专用页面，至少兼容IE8。

 

### 2、屏幕分辨率兼容策略

屏幕分辨率最少要考虑兼容便携屏幕和移动屏幕两种。可以参考去哪儿网的做法，把内容分成三类：移动端主菜单与导航栏；主要内容；扩展内容。屏幕分辨率高于480，显示主要内容、扩展内容。屏幕分辨率低于480，显示移动端主菜单与导航栏、主要内容。

 

如果你的应用是管理软件，则最好考虑兼容桌面屏幕、便携屏幕和移动屏幕三种。Bootstrap5新增了超超大屏幕，则就是基于这种考虑。这时候，可以加入侧边栏自动隐藏/打开，主要内容用Flex方式组织，可以在页面中并排显示多页（类似于Word的页面视图）。

 

### 3、跨平台兼容策略

大型网站，手机网站与桌面网站是不同的入口，因此不存在兼容，是两个单独的应用程序。对于流量较小的网站，平台的兼容策略主要是应用响应式框架，加上移动端主菜单与导航栏即可，其次可以选用跨平台框架来实现在不同平台的差异化体验。没有这些框架对于Web网站来说不造成大的体验下降。而如果需要开发混合移动、桌面应用，则需要认真考虑这些框架，毕竟用户对本地应用的体验期待要高很多。
