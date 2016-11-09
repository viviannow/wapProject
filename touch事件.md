touch事件touch是针对触屏手机上的触摸事件。现今大多数触屏手机webkit内核提供了touch事件的监听，让开发者可以获取用户触摸屏幕时的一些信息。

市面上很多框架都针对手机浏览器封装了这些手势，例如jqmobile、zepto(fastclick)、jqtouch.


github上有一个叫做fastclick的库，它也能规避移动设备上click事件的延迟响应，https://github.com/ftlabs/fastclick
将它用script标签引入页面（该库支持AMD，于是你也可以按照AMD规范，用诸如require.js的模块加载器引入），并且在dom ready时初始化在body上，如：
```
$(function(){
 new FastClick(document.body);
})
```
然后给需要“无延迟点击”的元素绑定click事件（注意不再是绑定zepto的tap事件）即可。
当然，你也可以不在body上初始化它，而在某个dom上初始化，这样，只有这个dom和它的子元素才能享受“无延迟”的点击
实践开发中发现，当元素绑定fastclick后，click响应速度比tap还要快一点点



### 手指在滑动整个屏幕时，会影响浏览器的行为，比如滚动和缩放。所以在调用touch事件时，要注意禁止缩放和滚动。
1.禁止缩放
通过meta元标签来设置。
2.禁止滚动
preventDefault是阻止默认行为，touch事件的默认行为就是滚动。
event.preventDefault();

### touch事件，一般用于移动端的触屏滑动

touchstart:当手指触摸屏幕时触发；即使已经有一个手指放在了屏幕上也会触发。
touchmove:当手指在屏幕上滑动时连续的触发。在这个事件发生期间，调用preventDefault()可阻止滚动。
touchend:当手指从屏幕上移开时触发。
touchcancel:当系统停止跟踪触摸时触发。关于此事件的确切触发事件，文档中没有明确说明

```
//阻止事件方法
document.body.addEventListener('touchmove', function(event) {
event.preventDefault();
}, false); 

//添加开关
document.addEventListener('touchmove', function(event) {
	//判断条件,条件成立才阻止背景页面滚动,其他情况不会再影响到页面滚动
	if(key == true){
		event.preventDefault();
	}
})
```
