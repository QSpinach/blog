#### reduce 问题
在ie下会出现Uint8Array 无法使用reduce方法，原因ie下Uint8Array不是一个数组集合而是一个对象集合
解决方法：使用lodash中的reduce，即可兼容Array|Object

==============================================================
#### 获取json对象的键和值
var data = {a: 1, b: 2, c: 3, d: 4}
Object.keys(data);  // ["a", "b", "c", "d"]
Object.values(data);    // [1, 2, 3, 4]

==============================================================
#### vscode 修饰报错 修改setting
"javascript.implicitProjectConfig.experimentalDecorators": true

==============================================================
#### 状态栏
window对象的defaultStatus
状态栏显示时间
d = new Date();
time = d.getHours();
window.status = time;

#### 盗链问题
```
var frontURL = document.referrer;
var host = location.hostname;
if(frontURL != ""){
	var frontHost = frontURL.substring(7.host.length + 7)
	if(host == frontHost){
		alert("没有盗链");
	}
	else{
		alert("非法盗链");
	}
}
else{
	alert("你是直接打开文档的");
}
```

#### 锚对象
window.document.anchors

#### 历史对象
history.go(n)
n=0表示载入当前页面，n>0表示载入历史列表中往前数第n个页面,n<0表示载入历史列表中的往后数第n个页面

#### 华氏温度和摄氏温度

```
var degFahren = prompt("Enter the degrees in Fahrenheit",50);
var degCent;
degCent = 5/9*(degFahren-32);
alert(degCent);
```

#### 数据类型转换

```
parseInt();
parseFloat();
for...in循环,无需知道数组的元素的个数
var elementIndex;
for(elementIndex in myArray){
	document.write(myArray[elementIndex]);
}
```

#### 阶乘

```
calcFactorial(num);
```

#### 在一个字符串中查找另一个字符串

```
indexOf();
```

#### 复制字符串的一个子串

```
var myString = "JavaScript";
var mySubString = myString.substring(0,4);
```

#### 转换大小写

```
toLowerCase()和toUpperCase()
```

#### 将字符编码转换为字符串 fromCharCode()方法

```
var myString = String.fromCharCode(65,66,67);
```

#### slice()方法，复制数组的部分

```
var names = new Array("Eggs","Milks","Potatoes");
var slicedArray = names.slice(1,3);
```

#### join()将数组转换为字符串

```
var myShopping = new Array("Eggs","Milks","Potatoes");
var myShooingList = myShopping.join("<br/>");
```

#### 按字母排序

```
var names = new Array("Eggs","Milks","Potatoes");
names.sort();
```

#### reverse()方法，反转数组元素的顺序

```
var myShopping = new Array("Eggs","Milks","Potatoes");
myShopping.reverse();
```

#### 测试元素

```
every();some();filter();
var num = new Array(1,2,3);
function Test(){}
every(Test);
```

#### abs();返回所传入的绝对值

```
var myNumber = -101;
document.write(Math.abs(myNumber));
```

ceil();修整到最接近的最小整数，即向上修整
floor();舍去小数部分
round();大于等于0.5向上修整，小于等于0.5向下修整

正则表达式
“g”表示全局标志

****************************************************************************************************************

***select改变值事件
```
	select.onchange = function(){};
```

***添加删除数组
	push()后面推进去
	   向数组的末尾添加一个或多个元素，并返回新的长度。
	unshift()从数组的前面放入
	   向数组的开头添加一个或更多元素，并返回新的长度
	pop() 删除最后一个数组元素
	shift()删除第一个数组元素
***数组和字符串转换
	join()将数组转换为字符串
	split()将字符串转换为数组
***插入子节点
	1. appendChild();    添加孩子     append 添加的意思
		意思：  添加孩子   放到盒子的 最后面。
	2. insertBefore(插入的节点，参照节点)   子节点  添加孩子
***克隆节点
	cloneNode();
	括号里面可以跟参数  ， 如果 里面是 true  深层复制， 除了复制本盒子，还复制子节点  
	如果为 false  浅层复制   只复制   本节点  不复制 子节点。

******url编码和解码
	encodeURIComponent()函数可把字符串作为URI组件进行编码
	decodeURIComponent()函数可把字符串作为URI组件进行解码
******substr()
	substr(起始位置,[取的个数])
	同上。  
  不写取的个数， 默认从起始位置一直取到最后 。
  取的个数：    是指从起始位置开始，往后面数几个。

*******offset家族
	offsetWidth  offsetHeight
	得到对象的宽度和高度(自己的，与他人无关) offsetWidth =  width  + border  +  padding
	offsetLeft   offsetTop
	返回距离上级盒子（最近的带有定位）左边的位置

******offsetTop
	var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;
******client
	clientX          clientWidth   可视区域的宽度 
	clientWidth     width  +  padding        
	offsetWidth     width + padding + border 
	scrollWidth     width + padding      超过  内容的宽度
******Math
	Math.ceil(); 向上取整
	Math.floor();向下取整
	Math.round();四舍五入
******获取css样式
	 1.   obj.currentStyle   ie  opera  常用
		外部（使用<link>）和内嵌（使用<style>）样式表中的样式（ie和opera）
	 2 .window.getComputedStyle("元素", "伪类")     w3c 两个选项是必须的， 没有伪类 用 null 替代
	 3.兼容
	 function getStyle(obj,attr) {
		if (obj.currentStyle) {
			return obj.currentStyle[attr];
		} else {
			return window.getComputedStyle(obj,null)[attr];
		}
	  }
*******in运算符
	in运算符也是一个二元运算符，但是对运算符左右两个操作数的要求比较严格。
	in运算符要求第1个（左边的）操作数必须是字符串类型或可以转换为字符串类型的其他类型，
	而第2个（右边的）操作数必须是数组或对象。只有第1个操作数的值是第2个操作数的属性名，
	才会返回true，否则返回false

*******************

#### js 内置对象：

```
	String 
	Date
	Math
	Array
	RegExp
	Number
	Object
	Function
	Null
	Boolean
	Error
	Cookie
	Session
```

#### Js Bom对象
```
	Window
	Document
	History
	Location
	Screen
	Navigator
```

#### 将伪数组转化为数组

```
	var json = {0:'first',1:'second',length:2};
	Array.prototype.slice.call(json);
```



#### 写一个通用的事件侦听器函数
// event(事件)工具集，来源：github.com/markyun

```
markyun.Event = {
    // 页面加载完成后
    readyEvent : function(fn) {
        if (fn==null) {
            fn=document;
        }
        var oldonload = window.onload;
        if (typeof window.onload != 'function') {
            window.onload = fn;
        } else {
            window.onload = function() {
                oldonload();
                fn();
            };
        }
    },
    // 视能力分别使用dom0||dom2||IE方式 来绑定事件
    // 参数： 操作的元素,事件名称 ,事件处理程序
    addEvent : function(element, type, handler) {
        if (element.addEventListener) {
            //事件类型、需要执行的函数、是否捕捉
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent) {
            element.attachEvent('on' + type, function() {
                handler.call(element);
            });
        } else {
            element['on' + type] = handler;
        }
    },
    // 移除事件
    removeEvent : function(element, type, handler) {
        if (element.removeEnentListener) {
            element.removeEnentListener(type, handler, false);
        } else if (element.detachEvent) {
            element.detachEvent('on' + type, handler);
        } else {
            element['on' + type] = null;
        }
    }, 
    // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
    stopPropagation : function(ev) {
        if (ev.stopPropagation) {
            ev.stopPropagation();
        } else {
            ev.cancelBubble = true;
        }
    },
    // 取消事件的默认行为
    preventDefault : function(event) {
        if (event.preventDefault) {
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },
    // 获取事件目标
    getTarget : function(event) {
        return event.target || event.srcElement;
    },
    // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
    getEvent : function(e) {
        var ev = e || window.event;
        if (!ev) {
            var c = this.getEvent.caller;
            while (c) {
                ev = c.arguments[0];
                if (ev && Event == ev.constructor) {
                    break;
                }
                c = c.caller;
            }
        }
        return ev;
    }
};

```

******************
Ajax 是什么？Ajax 的交互模型？同步和异步的区别？如何解决跨域问题？
Ajax 是什么：
1. 通过异步模式，提升了用户体验
2. 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用
3. Ajax 在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。

Ajax 的最大的特点：
1. Ajax可以实现动态不刷新（局部刷新）
2. readyState 属性 状态 有5个可取值： 0 = 未初始化，1 = 启动， 2 = 发送，3 = 接收，4 = 完成

Ajax 同步和异步的区别:
1. 同步：提交请求 -> 等待服务器处理 -> 处理完毕返回，这个期间客户端浏览器不能干任何事
2. 异步：请求通过事件触发 -> 服务器处理（这是浏览器仍然可以作其他事情）-> 处理完毕
ajax.open方法中，第3个参数是设同步或者异步。

Ajax 的缺点：
1. Ajax 不支持浏览器 back 按钮
2. 安全问题 Ajax 暴露了与服务器交互的细节
3. 对搜索引擎的支持比较弱
4. 破坏了程序的异常机制
5. 不容易调试

解决跨域问题：
1. jsonp
2. iframe
3. window.name、window.postMessage
4. 服务器上设置代理页面

```
*************************************

function whatBrowser() {  
    document.Browser.Name.value=navigator.appName;  
    document.Browser.Version.value=navigator.appVersion;  
    document.Browser.Code.value=navigator.appCodeName;  
    document.Browser.Agent.value=navigator.userAgent;  
}
/*
* 智能获取浏览器版本信息
*
*/
var browser={
    versions:function(){
    var u = navigator.userAgent, app = navigator.appVersion;
    return {//移动终端浏览器版本信息
      trident: u.indexOf('Trident') > -1, //IE内核
      presto: u.indexOf('Presto') > -1, //opera内核
      webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核
      gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1, //火狐内核
      mobile: !!u.match(/AppleWebKit.*Mobile.*/)||!!u.match(/AppleWebKit/), //是否为移动终端
      ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios终端
      android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android终端或者uc浏览器
      iPhone: u.indexOf('iPhone') > -1 || u.indexOf('Mac') > -1, //是否为iPhone或者QQHD浏览器
      iPad: u.indexOf('iPad') > -1, //是否iPad
      webApp: u.indexOf('Safari') == -1 //是否web应该程序，没有头部与底部
    };
   }(),
   language:(navigator.browserLanguage || navigator.language).toLowerCase()
}

```

****************状态码
100 Continue  继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
200 OK   正常返回信息
201 Created  请求成功并且服务器创建了新的资源
202 Accepted  服务器已接受请求，但尚未处理
301 Moved Permanently  请求的网页已永久移动到新位置
302 Found  临时性重定向
303 See Other  临时性重定向，且总是使用 GET 请求新的 URI
304 Not Modified  自从上次请求后，请求的网页未修改过
400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求
401 Unauthorized  请求未授权
403 Forbidden  禁止访问
404 Not Found  找不到如何与 URI 相匹配的资源
500 Internal Server Error  最常见的服务器端错误
503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）

**********************js 操作获取和设置 cookie
// 创建cookie
```
function setCookie(name, value, expires, path, domain, secure) {
    var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
    if (expires instanceof Date) {
        cookieText += '; expires=' + expires;
    }
    if (path) {
        cookieText += "; path=" + path     }
    if (domain) {
        cookieText += '; domain=' + domain;
    }
    if (secure) {
        cookieText += '; secure';
    }
    document.cookie = cookieText;
}
// 获取cookie
function getCookie(name) {
    var cookieName = encodeURIComponent(name) + '=';
    var cookieStart = document.cookie.indexOf(cookieName);
    var cookieValue = null;
    if (cookieStart > -1) {
        var cookieEnd = document.cookie.indexOf(';', cookieStart);
        if (cookieEnd == -1) {
            cookieEnd = document.cookie.length;
        }
        cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
    }
    return cookieValue;
}
// 删除cookie
function unsetCookie(name) {
    document.cookie = name + "= ; expires=" + new Date(0);
}
```

**************************************************************
			ES6
**************************************************************
----模板字符串：
    let apple = "苹果";
    let coffee = "咖啡";
    let = kitChen`今天的早餐是${apple} 与 ${coffee} !`;
    function kitChen(strings, ...values) {
	console.log(strings); // ["今天的早餐是", "与", "!", raw: Array[3]]
	consloe.log(values);  // ["苹果", "咖啡"]
    }

----新字符串方法
    let breakfast = "今天早餐是什么？";
    console.log(breakfast.startsWith("今天")); // true 判断以什么开头
    console.log(breakfast.endsWith("!")); // false 判断以什么结尾
    console.log(breakfast.includes("?")); // true 判断是否包含

----设置函数默认参数
    function breakfast(coke = "蛋糕", drink = "果汁") {
	return `${coke} , ${drink}`;
    }
    console.log(breakfast());

----展开操作符
    let fruits = ["苹果", "香蕉"],
	foods = ["橘子", ...fruits];
    console.log(foods); // ["橘子", "苹果", "香蕉"]

----函数name
    let breakfast = function(){}
    console.log(breakfast.name); // breakfast
    let breakfast = function superBreakfast(){}
    console.log(breakfast.name); // superBreakfast

----判断两个值是否相等
    Object.is(NaN, NaN); // true
    Object.is(+0, -0); // false

----把一个对象值复制到另一个对象
    let breakfast = {};
    breakfast.assgin(breakfast, {drink: "啤酒"})

----设置对象的prototype
    let breakfast = { getDrink(){ return "果汁"; }};
    let dinner = { getDrink(){ return "啤酒";}};
    let sunday = Object.create(breakfast); // 基于breakfast创建的对象
    console.log(Object.getPrototypeOf(sunday) === breakfast); // true
    Object.setProtytypeOf(sunday, dinner); ****
    console.log(Object.getPrototypeOf(sunday) === dinner); // true

---- __proto__
    let breakfast = { getDrink(){ return "果汁"; }};
    let dinner = { getDrink(){ return "啤酒";}};
    let sunday = { __proto__: breakfast };
    console.log(Object.getPrototypeOf(sunday) === breakfast); // true
    sunday.__proto__ = dinner;
    console.log(Object.getPrototypeOf(sunday) === dinner); // true

----super
    let breakfast = { getDrink(){ return "果汁"; }};
    let dinner = { getDrink(){ return "啤酒";}};
    let sunday = { __proto__: breakfast, getDrink(){ return super.getDrink() + "牛奶"; } };
    console.log(sunday.getDrink()); // "果汁牛奶"



*****************************************************************************************
问题：判断select选择情况
*****************************************************************************************
```
$("#demo").change(function () {
    var val = $(this).val();
    var res = confirm("您确认修改为"+val+"么？");
    if(res == true){
        //确认
        $(this).attr("hook",val);
    }else{
        //取消
        if(typeof $(this).attr("hook") == "undefined"){
            //尚未做过选择，重置为默认选择
            $(this).val($(this).children("option:first-child").val());
        }else{
            //重置为修改之前的选择
            $(this).val($(this).attr("hook"));
        }
    }
});
```

*************************************************************
时间format
*************************************************************

```
//格式化CST日期的字串
function formatCSTDate(strDate, format) {
    return formatDate(new Date(strDate), format);
}
//格式化日期
function formatDate(date, format) {
    var paddNum = function (num) {
        num += "";
        return num.replace(/^(\d)$/, "0$1");
    }
    //指定格式字符
    var cfg = {
        yyyy: date.getFullYear() //年 : 4位
        , yy: date.getFullYear().toString().substring(2)//年 : 2位
        , M: date.getMonth() + 1  //月 : 如果1位的时候不补0
        , MM: paddNum(date.getMonth() + 1) //月 : 如果1位的时候补0
        , d: date.getDate()   //日 : 如果1位的时候不补0
        , dd: paddNum(date.getDate())//日 : 如果1位的时候补0
        , hh: date.getHours()  //时
        , mm: date.getMinutes() //分
        , ss: date.getSeconds() //秒
    }
    format || (format = "yyyy-MM-dd hh:mm:ss");
    return format.replace(/([a-z])(\1)*/ig, function (m) {
        return cfg[m];
    });
}
```






