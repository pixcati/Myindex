
<h2 align="center">🌈 一个清新、简易的个人引导页</h2>
<hr>

![截图][1]
## 浏览
[https://www.svvme.com][2]
<br>
[https://www.svvme.com/index_vid.html   （加入视频背景）  ][3]

## 关于
一个简易的个人主页，样式仿 [iro 主题](https://iro.tw/)。


## 素材


#### 轻雨图标包
[APK](https://www.coolapk.com/apk/me.morirain.dev.iconpack.pure) |  [iCO](http://pan.svvme.com/download/60a62c23d57eff002b354d03)  | [PNG](http://pan.svvme.com/download/60a62c23d57eff002b354d02)


#### PACE加载特效
[Demo](https://codebyzach.github.io/pace/) | [Github](https://github.com/CodeByZach/pace)
```
<script src="https://cdn.jsdelivr.net/gh/pixcati/Myindex@main/pace.min.js" type="text/javascript"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/pixcati/Myindex@main/pace.css">

<script src="https://cdn.jsdelivr.net/npm/jquery@2.2.4/dist/jquery.min.js" type="text/javascript"></script>


<style type="text/css">
#遮罩 {
	padding: 0px;
	margin: 0px;
	top: -10%;
	left: -10%;
	width: 150%;
	height: 150%;
	position: fixed;
	display: inline-block;
	background-color: #fff;
	z-index: 100;
}
</style>

<script type="text/javascript">
			// PACE载完移除遮罩
			if(typeof Pace != 'undefined'){
				Pace.on('hide', function(){
					$("#遮罩").fadeOut(500,function(){
						$(this).remove();
					});
				});
}
</script>


```


#### 背景视频
 [笔记](https://github.com/pixcati/vidbg/blob/master/README.md) | [Github](https://github.com/blakewilson/vidbg)
```
<script src="https://cdn.jsdelivr.net/npm/jquery@2.2.4/dist/jquery.min.js" type="text/javascript"></script>
<script src="https://cdn.jsdelivr.net/gh/pixcati/vidbg@1.1.1/dist/vidbg.js" type="text/javascript"></script>



<div class="样式" data-vidbg-bg="mp4: 视频地址, 
                 webm: 视频地址"
  data-vidbg-options="loop: false, muted: false, overlay: true, overlayAlpha: 0.0 ">

</div>


```

#### 播放器
[笔记](https://github.com/pixcati/MetingJS) | [Aplayer][4] | [MetingJS][5]


#### 点击特效
```
<script type="text/javascript">
function clickEffect() {
let balls = [];
let longPressed = false;
let longPress;
let multiplier = 0;
let width, height;
let origin;
let normal;
let ctx;
const colours = ["#F73859", "#14FFEC", "#00E0FF", "#FF99FE", "#FAF15D"];
const canvas = document.createElement("canvas");
document.body.appendChild(canvas);
canvas.setAttribute("style",
"width: 100%; height: 100%; top: 0; left: 0; z-index: 99999; position: fixed; pointer-events: none;");
const pointer = document.createElement("span");
pointer.classList.add("pointer");
document.body.appendChild(pointer);
if (canvas.getContext && window.addEventListener) {
ctx = canvas.getContext("2d");
updateSize();
window.addEventListener('resize', updateSize, false);
loop();
window.addEventListener("mousedown", function(e) {
pushBalls(randBetween(10, 20), e.clientX, e.clientY);
document.body.classList.add("is-pressed");
longPress = setTimeout(function() {
document.body.classList.add("is-longpress");
longPressed = true;
}, 500);
}, false);
window.addEventListener("mouseup", function(e) {
clearInterval(longPress);
if (longPressed == true) {
document.body.classList.remove("is-longpress");
pushBalls(randBetween(50 + Math.ceil(multiplier), 100 + Math.ceil(multiplier)), e.clientX, e.clientY);
longPressed = false;
}
document.body.classList.remove("is-pressed");
}, false);
window.addEventListener("mousemove", function(e) {
let x = e.clientX;
let y = e.clientY;
pointer.style.top = y + "px";
pointer.style.left = x + "px";
}, false);
} else {
console.log("canvas or addEventListener is unsupported!");
}

function updateSize() {
canvas.width = window.innerWidth * 2;
canvas.height = window.innerHeight * 2;
canvas.style.width = window.innerWidth + 'px';
canvas.style.height = window.innerHeight + 'px';
ctx.scale(2, 2);
width = (canvas.width = window.innerWidth);
height = (canvas.height = window.innerHeight);
origin = {
x: width / 2,
y: height / 2
};
normal = {
x: width / 2,
y: height / 2
};
}
class Ball {
constructor(x = origin.x, y = origin.y) {
this.x = x;
this.y = y;
this.angle = Math.PI * 2 * Math.random();
if (longPressed == true) {
this.multiplier = randBetween(14 + multiplier, 15 + multiplier);
} else {
this.multiplier = randBetween(6, 12);
}
this.vx = (this.multiplier + Math.random() * 0.5) * Math.cos(this.angle);
this.vy = (this.multiplier + Math.random() * 0.5) * Math.sin(this.angle);
this.r = randBetween(8, 12) + 3 * Math.random();
this.color = colours[Math.floor(Math.random() * colours.length)];
}
update() {
this.x += this.vx - normal.x;
this.y += this.vy - normal.y;
normal.x = -2 / window.innerWidth * Math.sin(this.angle);
normal.y = -2 / window.innerHeight * Math.cos(this.angle);
this.r -= 0.3;
this.vx *= 0.9;
this.vy *= 0.9;
}
}

function pushBalls(count = 1, x = origin.x, y = origin.y) {
for (let i = 0; i < count; i++) {
balls.push(new Ball(x, y));
}
}

function randBetween(min, max) {
return Math.floor(Math.random() * max) + min;
}

function loop() {
ctx.fillStyle = "rgba(255, 255, 255, 0)";
ctx.clearRect(0, 0, canvas.width, canvas.height);
for (let i = 0; i < balls.length; i++) {
let b = balls[i];
if (b.r < 0) continue;
ctx.fillStyle = b.color;
ctx.beginPath();
ctx.arc(b.x, b.y, b.r, 0, Math.PI * 2, false);
ctx.fill();
b.update();
}
if (longPressed == true) {
multiplier += 0.2;
} else if (!longPressed && multiplier >= 0) {
multiplier -= 0.4;
}
removeBall();
requestAnimationFrame(loop);
}

function removeBall() {
for (let i = 0; i < balls.length; i++) {
let b = balls[i];
if (b.x + b.r < 0 || b.x - b.r > width || b.y + b.r < 0 || b.y - b.r > height || b.r < 0) {
balls.splice(i, 1);
}
}
}
}
clickEffect();
</script>

```


  [1]: https://s3.jpg.cm/2021/05/20/OCq65.jpg
  [2]: https://www.svvme.com/
  [3]: https://www.svvme.com/index_vid.html
  [4]: https://aplayer.js.org/
  [5]: https://github.com/metowolf/MetingJS
