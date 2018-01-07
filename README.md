# Web mobile layout - Review

## 1. 回顾移动端布局
## 2. 原生js模拟less正则匹配实现rem换算

### 3. 使用方法

```
git clone https://github.com/RiversCoder/mobile_layout.git

cd mobile_layout 
```

> 1. meta设置

```
<meta name='viewport' content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />
<meta name="x5-orientation" content="portrait">
```


> 2. 移动端布局中html根元素的fontSize换算

```js
function getSize(){
	let html = window.documentElement|| document.getElementsByTagName('html')[0];
	let htmlWidth = html.clientWidth;

	let fontSize = htmlWidth/15; //相当于把当前页面分成了15份
	html.style.fontSize = fontSize + 'px';
	
	return  fontSize;
}
```

> 3. 自定义css (用rpx当作计量单位)

```html
<style type="text/css" id="myStyle">
	...
	.header{width:100%;height:128rpx;background:#fff;border-bottom:1px solid #eee;}
	.header .h_left{width:107rpx;height:100%;background-image:url(./images/header_back.jpg);background-size:100% 100%; background-repeat:no-repeat;float:left;}
	.header .h_title{width:544rpx;height:100%;font-size:41rpx;text-transform:uppercase;text-align:center;line-height:128rpx;color:#3a3a3a;float:left;}
	...
</style>	
```

> 4. rpx换算成rem

```js
let myStyle = document.getElementById('myStyle');
var str = myStyle.innerHTML;
let regExp = /\s*(\d+\s*rpx)/gi;

var proportion = Number.parseInt(750/15) ;  //设计图尺寸750px 所以需要把设计图分成15份
var strs = str.replace(regExp,($0,$1) => {
	return (Number.parseInt($1)/proportion) + 'rem ';
})
myStyle.innerHTML = strs;
```

> 5. 最终渲染结果

![image](/images/render_finish_small.jpg)