# 网页版本下拉刷新

------

手机APP开发中，下拉刷新是一个很常见的功能，但是在网页中，这种模式用的很少。网页下拉刷新，看似简单的功能，但我在网上并没有找到比较好的解决方法。自己开发了一个，期间遇到了各种小坑，浏览器兼容，各种浏览器下拉默认事件，PC端无触摸事件~。记录一下

### 简单效果图
![下拉刷新效果图](res/demo.gif)


## 静态样式
**html代码示例**
```html
<div class="container" id="container">
	<div class="loading-warp">
	</div>
</div>
```
其中container是触摸容器，loading-warp，是刷新提示容器，容器样式、id可以自定义，此处只是示例而已

**css代码示例**
```css
.container{ overflow: hidden; min-height: 100%; }
.loading-warp{ margin-top: -100px; }
```
container高度不能设置为0,以免不能触发触摸事件，overflow属性必须设置为hidden~
loading-warp的margin-top值必须设置为其自身高度的相反值~

## 引用
```javascript
<script type="text/javascript" src="script/lib/jquery-1.11.0.js"></script>
<script type="text/javascript" src="script/p-pull-refresh.js"></script>
```
WAP端引入jquery与下拉插件即可，当然也可以引用zepto

```javascript
<script type="text/javascript" src="script/lib/jquery-1.11.0.js"></script>
<script type="text/javascript" src="script/lib/touche.js"></script>
<script type="text/javascript" src="script/p-pull-refresh.js"></script>
```
- PC端需要额外引入touche库文件添加触摸支持 [touche](https://github.com/pyrinelaw/touche);
- PC端调用需要触摸容器中图片相关元素的draggable为false，否则会触发默认拖动事件，导致下拉刷新失败;

## 调用参数
```javascript
{
     // 触摸容器，默认为body
    $el: $('body'),	   
    // 刷新提示容器
    $loadingEl: null,
    // 是否自动隐藏
    autoHide: true, 
    // 获取下拉刷新发送数据，可以使用静态数据，也可以使用使用function动态传入数据
    sendData: null,	    
    // 触发拖动像素距离(触发灵敏度),
    // 浏览器中下拉默认事件一旦触发后，就不能再通过冒泡阻止此事件。
    // chrome浏览器中大概是15PX左右的下拉后触发默认刷新，微信中大概是6像素左右。
    // 如需在微信中使用，建议设置为6像素
    startPX: 6, 	
    // 回调函数
    callbacks: {
    	pullStart: null,	// 拖动开始
    	start: null,	// 开始请求数据
    	success: null,	// 数据请求成功
    	error: null,	// 数据请求错误
    	end: null,	// 下拉流程结束
    }
}
```
## 提供方法
```javascript
// 初始化
reset();
// 设置销毁状态,statu设置为false后下拉刷新将不再生效，设置为true后将再次生效
setDestroy(statu);
```

### 相关资料
下载地址: [https://github.com/pyrinelaw/p-pull-refresh](https://github.com/pyrinelaw/p-pull-refresh)
Demo: [http://pyrinelaw.github.io/pRefresh](http://pyrinelaw.github.io/pRefresh)
Drag介绍文档: [http://www.w3schools.com/tags/ev_ondrag.asp](http://www.w3schools.com/tags/ev_ondrag.asp)
作者: [Petrus.Law](https://github.com/pyrinelaw)

---
创建日期: 2015/11/12