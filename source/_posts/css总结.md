---
tags: [css]
comments: true
toc: true
---



### 浮动

牛客：
(1)、父级div定义 height 
原理：父级div手动定义height，就解决了父级div无法自动获取到高度的问题。 
优点：简单、代码少、容易掌握 
缺点：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题 
建议：不推荐使用，只建议高度固定的布局时使用 
(2)、结尾处加空div标签 clear:both 
原理：添加一个空div，利用css提高的clear:both清除浮动，让父级div能自动获取到高度 
优点：简单、代码少、浏览器支持好、不容易出现怪问题 
缺点：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不好 
建议：不推荐使用，但此方法是以前主要使用的一种清除浮动方法 
(3)、父级div定义 伪类:after 和 zoom 
原理：IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题 
优点：浏览器支持好、不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等） 
缺点：代码多、不少初学者不理解原理，要两句代码结合使用才能让主流浏览器都支持。 
建议：推荐使用，建议定义公共类，以减少CSS代码。
(4)、父级div定义 overflow:hidden 
原理：必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度 
优点：简单、代码少、浏览器支持好 
缺点：不能和position配合使用，因为超出的尺寸的会被隐藏。 
建议：只推荐没有使用position或对overflow:hidden理解比较深的朋友使用。 
(5)、父级div定义 overflow:auto 
原理：必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度 
优点：简单、代码少、浏览器支持好 
缺点：内部宽高超过父级div时，会出现滚动条。 
建议：不推荐使用，如果你需要出现滚动条或者确保你的代码不会出现滚动条就使用吧。

传智：
1） 加高法
2)  clear:both;
3)  隔墙法

	<div>
		<p></p>
		<p></p>
		<p></p>
	</div>
	<div class="cl h10"></div>
	<div>
		<p></p>
		<p></p>
		<p></p>
	</div>

4） 内墙法

	<div>
		<p></p>
		<p></p>
		<p></p>
		<div class="cl h10"></div>
	</div>
	<div>
		<p></p>
		<p></p>
		<p></p>
	</div>
5） overflow:hidden;



### IE6兼容浮动
IE6留了一个后门，就是只要给css属性之前，加上下划线，这个属性就是IE6认识的专有属性。
	_background-color: green;
第二，IE6不支持用overflow:hidden;来清除浮动的
解决办法，以毒攻毒。追加一条
	_zoom:1;

### margin
1、塌陷问题
2、对其方式
必须有width 才能使用margin：0 auto;
3、善于使用父亲的padding，而不是儿子的margin
4、关于margin的IE6兼容问题
	当出现连续浮动的元素，携带和浮动方向相同的margin时，队首的元素，会双倍marign。
	解决方案：1、设置与浮动相反的margin
		  2、给首元素加：_margin-left

### 超链接
1、记住，这四种状态，在css中，必须按照固定的顺序写：
a:link 、a:visited 、a:hover 、a:active
2、所有的a不继承text、font这些东西。因为a自己有一个伪类的权重。

### background
1、背景是否固定。background-attachment:fixed;

### position
1、绝对定位的儿子，无视参考的那个盒子的padding。
2、不一定是相对定位，任何定位，都可以作为参考点
3、绝对定位的盒子居中
	margin:0 auto;失效。
	left:50%; margin-left:负的宽度的一半。
4、固定定位
	IE6不兼容。

### z-index
1、只有定位了的元素，才能有z-index值。也就是说，不管相对定位、绝对定位、固定定位，都可以使用z-index值。
   而浮动的东西不能用。
2、从父现象：父亲怂了，儿子再牛逼也没用。

***
### 常见的浏览器兼容性解决方案
(1)浏览器兼容问题一：不同浏览器的标签默认的外补丁和内补丁不同 
问题症状：随便写几个标签，不加样式控制的情况下，各自的margin 和padding差异较大。
碰到频率:100%
解决方案：CSS里 *{margin:0;padding:0;}
备注：这个是最常见的也是最易解决的一个浏览器兼容性问题，几乎所有的CSS文件开头都会用通配符*来设置各个标签的内外补丁是0。
(2)浏览器兼容问题二：块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大 
问题症状:常见症状是IE6中后面的一块被顶到下一行
碰到频率：90%（稍微复杂点的页面都会碰到，float布局最常见的浏览器兼容问题）
解决方案：在float的标签样式控制中加入 display:inline;将其转化为行内属性
备注：我们最常用的就是div+CSS布局了，而div就是一个典型的块属性标签，横向布局的时候我们通常都是用div float实现的，横向的间距设置如果用margin实现，这就是一个必然会碰到的兼容性问题。
(3)浏览器兼容问题三：设置较小高度标签（一般小于10px），在IE6，IE7，遨游中高度超出自己设置高度 
问题症状：IE6、7和遨游里这个标签的高度不受控制，超出自己设置的高度
碰到频率：60%
解决方案：给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。
备注：这种情况一般出现在我们设置小圆角背景的标签里。出现这个问题的原因是IE8之前的浏览器都会给标签一个最小默认的行高的高度。即使你的标签是空的，这个标签的高度还是会达到默认的行高。
(4)浏览器兼容问题四：行内属性标签，设置display:block后采用float布局，又有横行的margin的情况，IE6间距bug 
问题症状：IE6里的间距比超过设置的间距
碰到几率：20%
解决方案 ： 在display:block;后面加入display:inline;display:table;
备注：行内属性标签，为了设置宽高，我们需要设置display:block;(除了input标签比较特殊)。在用float布局并有横向的margin后，在IE6下，他就具有了块属性float后的横向margin的bug。不过因为它本身就是行内属性标签，所以我们再加上display:inline的话，它的高宽就不可设了。这时候我们还需要在display:inline后面加入display:talbe。
(5) 浏览器兼容问题五：图片默认有间距 
问题症状：几个img标签放在一起的时候，有些浏览器会有默认的间距，加了问题一中提到的通配符也不起作用。
碰到几率：20%
解决方案：使用float属性为img布局
备注 ： 因为img标签是行内属性标签，所以只要不超出容器宽度，img标签都会排在一行里，但是部分浏览器的img标签之间会有个间距。去掉这个间距使用float是正道。（我的一个学生使用负margin，虽然能解决，但负margin本身就是容易引起浏览器兼容问题的用法，所以我禁止他们使用）
(6) 浏览器兼容问题六：标签最低高度设置min-height不兼容 
问题症状：因为min-height本身就是一个不兼容的CSS属性，所以设置min-height时不能很好的被各个浏览器兼容
碰到几率：5%
解决方案：如果我们要设置一个标签的最小高度200px，需要进行的设置为：{min-height:200px; height:auto !important; height:200px; overflow:visible;}
备注：在B/S系统前端开时，有很多情况下我们又这种需求。当内容小于一个值（如300px）时。容器的高度为300px；当内容高度大于这个值时，容器高度被撑高，而不是出现滚动条。这时候我们就会面临这个兼容性问题。
(7)浏览器兼容问题七：透明度的兼容CSS设置 
一般在ie中用的是filter:alpha(opacity=0);这个属性来设置div或者是块级元素的透明度，而在firefox中，一般就是直接使用opacity:0,对于兼容的，一般的做法就是在书写css样式的将2个都写上就行，就能实现兼容

***
### 天猫 使用的css reset重置浏览器默认样式：
```
@charset "gb2312";body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td {margin: 0;padding: 0}body, button, input, select, textarea {font: 12px "microsoft yahei";line-height: 1.5;-ms-overflow-style: scrollbar}h1, h2, h3, h4, h5, h6 {font-size: 100%}ul, ol {list-style: none}a {text-decoration: none;cursor:pointer}a:hover {text-decoration: underline}img {border: 0}button, input, select, textarea {font-size: 100%}table {border-collapse: collapse;border-spacing: 0}.clear {clear:both}.fr {float:right}.fl {float:left}.block {display:block;text-indent:-999em}
```
***

### 网站重构
网站重构：在不改变外部行为的前提下，简化结构、添加可读性，而在网站前端保持一致的行为。也就是说是在不改变 UI 的情况下，对网站进行优化，在扩展的同时保持一致的 UI。

对于传统的网站来说重构通常是：
1. 表格(table)布局改为 DIV + CSS
2. 使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对 IE6 有效的)
3. 对于移动平台的优化
4. 针对于 SEO 进行优化
5. 深层次的网站重构应该考虑的方面
6. 减少代码间的耦合
7. 让代码保持弹性
8. 严格按规范编写代码
9. 设计可扩展的API
10. 代替旧有的框架、语言(如VB)
11. 增强用户体验
12. 通常来说对于速度的优化也包含在重构中
13. 压缩JS、CSS、image等前端资源(通常是由服务器来解决)
14. 程序的性能优化(如数据读写)
15. 采用CDN来加速资源加载
16. 对于JS DOM的优化
17. HTTP服务器的文件缓存