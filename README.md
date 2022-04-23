
<h2 align="center">一个简易的个人引导页</h2>
<hr>

![截图](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-803e33e7-38ec-4da2-8775-56918cd7c73b/69746f47-c430-4115-98be-315a01199065.png)
## 浏览

<h3 style="color:#5b94b1">继续完善、学习中。代码尚不规范成熟，仓库里都是黑历史</h3>

[svvme.com](https://www.svvme.com/)
<br>
[svvme.com/index_old2.html](https://www.svvme.com/index_old2.html)（加入视频背景,部分浏览器不可用）  

## 关于

一个简易的个人主页，样式仿 [iro 主题](https://iro.tw/)。


## 素材


#### 轻雨图标包
[APK](https://www.coolapk.com/apk/me.morirain.dev.iconpack.pure) |  [iCO](http://pan.svvme.com/index2.php?/%E5%9B%BE%E7%89%87%E3%80%81%E5%9B%BE%E6%A0%87/Pure%E8%BD%BB%E9%9B%A8%E5%9B%BE%E6%A0%87ico%E6%A0%BC%E5%BC%8F.zip?p=t)  | [PNG](http://pan.svvme.com/index2.php?/%E5%9B%BE%E7%89%87%E3%80%81%E5%9B%BE%E6%A0%87/Pure%E8%BD%BB%E9%9B%A8%E5%9B%BE%E6%A0%87png%E6%A0%BC%E5%BC%8F.zip?p=t)


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

#### 随机背景图
##### PHP
```
<?php
//存有链接的文件名
$filename = "pcls.txt";
if(!file_exists($filename)){
	die('文件不存在');
}

//从文本获取链接
$pics = [];
$fs = fopen($filename, "r");
while(!feof($fs)){
	$line=trim(fgets($fs));
	if($line!=''){
		array_push($pics, $line);
	}
}

//从数组随机获取链接
$pic = $pics[array_rand($pics)];

//返回指定格式
$type=$_GET['type'];
switch($type){

//JSON返回
case 'json':
	header('Content-type:text/json');
	die(json_encode(['pic'=>$pic]));

default:
	die(header("Location: $pic"));
}

```


#### 今日诗词API
[官网](https://www.jinrishici.com/)  | [API](https://www.jinrishici.com/doc/#json-fast)


#### Layui / Layer弹出层
[官网](https://www.layui.com/) | [Layer](https://layer.layui.com/)

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
[笔记](https://github.com/pixcati/MetingJS) | [Aplayer](https://aplayer.js.org/) | [MetingJS](https://github.com/metowolf/MetingJS)


#### 点击特效
```
<script type="text/javascript">
function clickEffect() {
    let balls = [];
    let longPressed = false;
    let longPress;
    let multiplier = 0;
    let width,
    height;
    let origin;
    let normal;
    let ctx;
    const colours = ["#F73859", "#14FFEC", "#00E0FF", "#FF99FE", "#FAF15D"];
    const canvas = document.createElement("canvas");
    document.body.appendChild(canvas);
    canvas.setAttribute("style", "width: 100%; height: 100%; top: 0; left: 0; z-index: 99999; position: fixed; pointer-events: none;");
    const pointer = document.createElement("span");
    pointer.classList.add("pointer");
    document.body.appendChild(pointer);
    if (canvas.getContext && window.addEventListener) {
        ctx = canvas.getContext("2d");
        updateSize();
        window.addEventListener('resize', updateSize, false);
        loop();
        window.addEventListener("mousedown",
        function(e) {
            pushBalls(randBetween(10, 20), e.clientX, e.clientY);
            document.body.classList.add("is-pressed");
            longPress = setTimeout(function() {
                document.body.classList.add("is-longpress");
                longPressed = true;
            },
            500);
        },
        false);
        window.addEventListener("mouseup",
        function(e) {
            clearInterval(longPress);
            if (longPressed == true) {
                document.body.classList.remove("is-longpress");
                pushBalls(randBetween(50 + Math.ceil(multiplier), 100 + Math.ceil(multiplier)), e.clientX, e.clientY);
                longPressed = false;
            }
            document.body.classList.remove("is-pressed");
        },
        false);
        window.addEventListener("mousemove",
        function(e) {
            let x = e.clientX;
            let y = e.clientY;
            pointer.style.top = y + "px";
            pointer.style.left = x + "px";
        },
        false);
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
