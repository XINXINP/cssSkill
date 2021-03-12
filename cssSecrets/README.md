
## 前言🐟
看《css揭秘》一书累积可以提高前端开发的一些样式（都是一些基础样式但是可以在此基础上不断丰富），发挥自己的的想像吧。
### 点赞支持👍
## 背景与边框🌼
### 1.扩大可点击区域
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e959924be20a46e79704de9362b2f1dc~tplv-k3u1fbpfcp-watermark.image)
````scss
//公共代码
section{max-height: 300px;min-height: 80px;}
div{width: 100px;height: 100px;}
::selection{background: red;}
.class2_1,.class2_2,.class2_3,.class5_1,.class5_2,.class5_3,.class5_4,.class5_5,.class5_6,.class6_1,.class6_2,.class8_1,.class8_2,.class8_3,.class8_4,
.class9_1,.class9_2,.class9_3,.class10_1,.class10_2,.class11_1,.class11_2,.class12_1,.class12_2,.class21_1,.class21_3,.class21_2{display: inline-block;margin: 10px;}
.mouse{position: fixed;right: 0;top:0;z-index: 5;width: 100px;height: 100px;}

//扩大可点击区域
//先定位再用after 然后在元素的后面插入 
@mixin expand-range($top: -10px, $right: $top, $bottom: $top, $left: $right, $position: relative) {
    position: $position;
    cursor: pointer;
    background: red;
    
    height: 30px;
    &:after {
      content: '';
      position: absolute;
      top: $top;
      right: $right;
      bottom: $bottom;
      left: $left;
}
}
.class1{@include expand-range($top: -5px, $position: absolute)}
````
### 2.box-shadow

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f71330c9b4f54fcfbfa9aa4500ac8e60~tplv-k3u1fbpfcp-watermark.image)
````scss
// ===========================================
@mixin bag1($clo1,$clo2,$clo3,$clo4) {
    box-shadow: 0 10px $clo1,10px 0px $clo2,-10px 0px $clo3,0px -10px $clo4;
}
//多重边框
@mixin bag2($clo1,$clo2,$clo3,$clo4) {
    box-shadow: inset 0 0 0 5px $clo1,0 0 0 5px $clo2,0 0 0 5px $clo3,0 0 0 5px $clo4;
}
// 描边
@mixin bag3($clo1) {
    outline: 10px solid $clo1;
    outline-offset: -10px;
}
.class2_1{background: #000;@include bag1(#888,#786,#346,#821);}
.class2_2{background: #000;@include bag2(#888,#786,#346,#821);}
.class2_3{background: #000;@include bag3(#821);}
````
### 3.box-position

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/30a55a9848734256ba4aad518002fb08~tplv-k3u1fbpfcp-watermark.image)
````scss
// =======================================================
// 灵活定位
@mixin pos1($img,$bag,$left,$right){
    background: url($img) no-repeat top center $bag;
    background-position: $left $right;
    background-size:20% 20% ;
}
.class3{@include pos1('../img/1.jpg',red,10px,20px)}
````
### 4.边框内圆角

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/57c37850ee874a609f346db0870a1fc5~tplv-k3u1fbpfcp-watermark.image)
````scss
// ==========================================================
// 利用伪元素边框内圆角
@mixin border($top: -10px, $right: $top, $bottom: $top, $left: $right, $position: relative) {
    position: $position;
    cursor: pointer;
    padding: $top;
    background: red;
    z-index: 1;
    &:after {
      content: '';
      background: orange;
      position: absolute;
      top: $top;
      right: $right;
      bottom: $bottom;
      left: $left;
      z-index: -1;
      border-radius: $top;
}
}
.class4{@include border(10px)}
````
### 5.简单条纹背景

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2e25a6a063b497199f93a074c900719~tplv-k3u1fbpfcp-watermark.image)
````scss
// ================================================================
// 简单条纹背景
//  linear-gradient与background-size
@mixin twen ($clo1,$clo2){
    background:  linear-gradient($clo1 50%,$clo2 50% );
    background-size: 100% 20%;
}
@mixin twen1 ($clo1,$clo2){
    background:  linear-gradient(134deg,$clo1 50%,$clo2 50% );
    background-size: 100% 20%;
}
@mixin twen2 ($clo1,$clo2){
    background:  linear-gradient(to right,$clo1 50%,$clo2 50% );
    background-size: 20% 100%;
}
@mixin twen3 ($clo1,$clo2){
    background:  linear-gradient(134deg,$clo1 50%,$clo2 50% );
    background-size: 20% 100%;
}
@mixin twen4 ($clo1,$clo2){
    background:  linear-gradient(134deg,$clo1 50%,$clo2 50% );
    background-size: 100% 20%;
}
@mixin twen5 ($clo1,$clo2){
    background:  linear-gradient(134deg,$clo1 50%,$clo2 50% );
    background-size: 20% 20%;
}
.class5_1{@include twen(red,orange)}
.class5_2{@include twen1(red,orange)}
.class5_3{@include twen2(red,orange)}
.class5_4{@include twen3(red,orange)}
.class5_5{@include twen4(red,orange)}
.class5_6{@include twen5(red,orange)}
````
### 6.复杂背景图

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9d0fd9c4c91543bf90c54c0905c985be~tplv-k3u1fbpfcp-watermark.image)
````scss
// ========================================================
// 复杂背景图案
@mixin fzbck($clo1) {
background-image:  linear-gradient(45deg,$clo1 30%,transparent 0),
     linear-gradient(45deg,transparent 75%,$clo1 0),
     linear-gradient(45deg,$clo1 25%,transparent 0),
     linear-gradient(45deg,transparent 75%,$clo1 0);
    background-size: 30% 30%;
}
@mixin fzbck1($clo1) {
    background-image:  linear-gradient(45deg,$clo1 30%,transparent 0), linear-gradient(to right,$clo1 30%,transparent 0), linear-gradient(75deg,$clo1 30%,transparent 0);
        background-size: 30% 30%;
    }
.class6_1{
    @include fzbck(#897)
}
.class6_2{
    @include fzbck1(#297)
}
````
### 7.蝉原则（周期动画）

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3ea09798970c4291aca266b9175912c9~tplv-k3u1fbpfcp-watermark.image)
````scss
// ====================================
@keyframes col{
    20%{background:orange;}
    60%{background: #897;}
}
@keyframes rad{
    50% {
        border-radius: 50%;
    }
}
@keyframes zhuan{
    100% {
        transform: rotate(360deg);
    }
}
.class7{border:10px solid red;background:#565;transform: .5s all;animation: col 2s infinite,rad 1s infinite,zhuan 1s infinite;}
````
### 8.好用的边框动画

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cfa705fe478e43d1a97022e3a4195d35~tplv-k3u1fbpfcp-watermark.image)
````scss
// ===================================================
.class8_1{
    background:  linear-gradient(white,white) padding-box,
    repeating-linear-gradient(-45deg,
    red 0,red 12.5%,
    transparent 0,transparent 25%,
    orange 0,orange 37.5%,
    transparent 0,transparent 50%) 0 / 5em 5em;
    border: 1em solid transparent;}
    .class8_2{
        background:  linear-gradient(white,white) padding-box,
        repeating-linear-gradient(-45deg,
        red 0,red 12.5%,
        transparent 0,transparent 25%,
        orange 0,orange 37.5%,
        transparent 0,transparent 50%) 0 / 5em 5em;
        border: 1em solid transparent;
        animation: 2s zhan1 infinite;
    }
    .class8_3{
        border: 1em solid transparent;
        animation: 2s zhan1 infinite;
        background:  linear-gradient(white,white) padding-box,
        repeating-linear-gradient(-45deg,
        black 0, black 25%,white 0, white 50%) 0 / 0.6em 0.6em;
    }
    .class8_4{
        border: 1px solid transparent;
        animation: 2s zhan1 infinite;
        background:  linear-gradient(white,white) padding-box,
        repeating-linear-gradient(-45deg,
        black 0, black 25%,white 0, white 50%) 0 / 0.6em 0.6em;
    }
        @keyframes zhan1{
            100%{background-position: 100%;}
        }
// ==================================================
````
## 形状🌲
### 9.自适应椭圆

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/496b8de01ffe44abbae99925a4cead11~tplv-k3u1fbpfcp-watermark.image)
````scss
// 自适应椭圆
.class9_1{
    background: red;
    border-radius: 50px;
}
.class9_2{
    background: red;
    border-radius: 50%/100% 100% 0 0 ;
}
.class9_3{
    background: red;
    border-radius: 50%/100% 100% 0 50%;
}
````
### 10.平行四边形

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4ba30c8e5e074da3928cede1a9cbf9cb~tplv-k3u1fbpfcp-watermark.image)
````scss
// ======================================
.class10_1{
    transform: skew(45deg);
    background: red;
}
.class10_1>div{
    transform: skew(-45deg);
}
.class10_2{
position: relative;
}
.class10_2:before{
    content: "";
    position: absolute;
    top: 0px;
    right: 0px;
    bottom: 0px;
    left: 0px;
    z-index: -1;
    background: orange;
    transform: skew(45deg);
}
````
### 11.菱形四边形

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/386980631bbd4b8288a5cb4fd9f016dc~tplv-k3u1fbpfcp-watermark.image)
````scss
// =======================================================
// 菱形四边形
.class11_1{
    background: red;
    transform: rotate(45deg);
}
.class11_1>div{
    transform: rotate(-45deg);
}
.class11_2{
    background: orange;
    transform: rotate(45deg);
}
.class11_2{
    clip-path: polygon(0 0,100% 0,100% 100%,0 100%);
    transition: 1s clip-path;
}
.class11_2:hover{
    clip-path: polygon(50% 0,100% 50%,50% 100%,0 50%);//图片裁剪
}
````
### 12.切角特效

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43e3dc0e45cc459b9621b403d53f36fc~tplv-k3u1fbpfcp-watermark.image)
````scss
// =========================================
//切角特效
.class12_1{background:  linear-gradient(45deg,transparent 20px,red 0);}//不涉及
.class12_2{	background: radial-gradient(circle at top left ,transparent 15px,red 0) top left,
    radial-gradient(circle at top right ,transparent 15px,red 0) top right,
    radial-gradient(circle at bottom right ,transparent 15px,red 0) bottom right,
    radial-gradient(circle at bottom left ,transparent 15px,red 0) bottom left;
    background-repeat: no-repeat;
    background-size: 50% 50%;
}
````
## 视觉特色🌊
### 13.投影1

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0207992aaa1f4968b28132245c6817ef~tplv-k3u1fbpfcp-watermark.image)
````scss
// ==================================
.class15{
    background: orange;
    box-shadow: 0 5px 4px -4px black;
}
````
### 14.投影2（悬浮颜色渐变）

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a4ac656c89cb42ffa3ecad9ed09f8b72~tplv-k3u1fbpfcp-watermark.image)
````scss
// ==========================================
.class17{
    transition:  1.5s filter;
    filter:sepia(1) saturate(1) hue-rotate(295deg);
    background: red;
}
.class17:hover{filter:none;}
````
### 15.毛玻璃

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cf91871325b84c659b38f69b0823625a~tplv-k3u1fbpfcp-watermark.image)
````scss
// =============================================
.class18{
background: url(../img/1.jpg) no-repeat top center;
background-size: 100%;
filter: blur(2px);
}
````
### 16.折角效果

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a6420cb38cb14d0eabf398c2af0d166e~tplv-k3u1fbpfcp-watermark.image)
````scss
// ================================================
// 折角效果
.class19{
background: blue;
background: linear-gradient(to left bottom,transparent 50%,orange 0) no-repeat 100% 0 / 21px 21px,
linear-gradient(-135deg,transparent 15px,red 0);
}
````
## 文字效果🍁
### 17.改变断行效果
![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ef7c57746fe94568bea416e233103dfa~tplv-k3u1fbpfcp-watermark.image)
````scss
// ================================================
// 不同浏览器效果不一样
.class20{
    width: 300px;
    hyphens: auto;
}
````
### 18.文字效果展示

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d580d6cd78ee4fbc9f35a9155670412a~tplv-k3u1fbpfcp-watermark.image)
````scss
// ===================================================
// 文字效果
//1text-shadow为文字添加阴影。可以为文字与  text-decorations  添加多个阴影，阴影值之间用逗号隔开。每个阴影值由元素在X和Y方向的偏移量、模糊半径和颜色值组成。
.class21_1{
    color: #fff;
    background: red;
    text-shadow: 1px 1px black,-1px -1px black,
    1px -1px black, -1px 1px black;
}
.class21_2{
    color: #fff;
    background: red;
    transform: .5s;
}
.class21_2:hover{
    filter: blur(1px);
}
.class21_3{
    color: #fff;
    font-size: 34px;
    display: block;
    background: red;
    text-align: center;
    text-shadow: 0 1px hsl(0,89%,85%),
    0 2px hsl(0,89%,80%),
    0 3px hsl(0,89%,75%),
    0 4px hsl(0,89%,70%),
    0 5px hsl(0,89%,65%),
    0 5px 10px black;
}
````
### 19.滚动效果💴

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b2996aeb0d2b40f6a84849fdc26e0b55~tplv-k3u1fbpfcp-watermark.image)
````scss
// ==============================================
.class22{
    overflow-y: auto;
    background: url(../img/1.jpg) no-repeat;
    background-size: 50px 50px;
    background-position: 20% 30%;
    background-attachment: local,scroll;
}
````
## 过渡动画🍃
### 20.打字效果

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6ef7ba856a734a7bb38dce7520ec43b1~tplv-k3u1fbpfcp-watermark.image)
````scss
// ====================================================
// 灵魂在于border-right
@keyframes typing {
    from {
        width: 0
    }
}

@keyframes caret {
    50% {
        border-right-color: transparent;
    }
}
.class23{
    max-width: 100%;
    width: 800px;
    height: 25px;
    white-space: nowrap;
    overflow: hidden;
    border-right: .05em solid;
    animation: typing 8s steps(100) infinite, caret 2s steps(1) infinite;
}
````
### 21.缓动效果

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/631c154061984ad1b305f51b8cd2d6da~tplv-k3u1fbpfcp-watermark.image)
````scss
// ==================================
.class24_1{
    background: green;
    position: relative;
}
.class24_2{
    width: 20px;height: 20px;border-radius: 50%;
    background: red;
    position: relative;
    animation: bounce 6s infinite ;
}
@keyframes bounce {
    60%,
    80%,
    to {
        transform: translateY(40px);
        animation-timing-function: ease;
    }
    70% {
        transform: translateY(50px);
    }
    90% {
        transform: translateY(60px);
    }
}
````
### 22.状态平衡动画

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/39c76bdf9bfa4ca68222401eddf01327~tplv-k3u1fbpfcp-watermark.image)
````scss
// ====================================================
// animation-play-state
@keyframes bk1{
    20%{background-position: 100% 100%;}
    40%{background-position: 0% 100%;}
    60%{background-position: 100% 0%;}
}
.class25{
    background: url(../img/1.jpg);
    animation: bk1 10s infinite;
    animation-play-state: paused;
    // background-size: auto 100%;
}
.class25:hover{animation-play-state: running;}
````
### 全部代码
- html代码
````html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>动画开发</title>
    <link rel="stylesheet" href="css/1.css">
</head>

<body>
    <section>
        <h1>背景与边框</h1>
        <p>1.扩大可点击区域</p>
        <div class="class1"></div>
    </section>
    <section>
        <p>2.box-shadow</p>
        <div class="class2_1"></div>
        <div class="class2_2"></div>
        <div class="class2_3"></div>
    </section>
    <section>
        <p>3.box-position</p>
        <div class="class3"></div>
    </section>
    <section>
        <p>4.边框内圆角</p>
        <div class="class4">利用::after</div>
    </section>
    <section>
        <p>5.简单条纹背景</p>
        <div class="class5_1"></div>
        <div class="class5_2"></div>
        <div class="class5_3"></div>
        <div class="class5_4"></div>
        <div class="class5_5"></div>
        <div class="class5_6"></div>
    </section>
    <section>
        <p>6.复杂的背景图</p>
        <div class="class6_1"></div>
        <div class="class6_2"></div>
    </section>
    <section>
        <p>7.蝉原则（周期动画）</p>
        <div class="class7"></div>
    </section>
    <section>
        <p>8.好用的边框动画</p>
        <div class="class8_1"></div>
        <div class="class8_2"></div>
        <div class="class8_3"></div>
        <div class="class8_4"></div>
    </section>
    <h1>形状</h1>
    <section>
        <p>9.自适应椭圆</p>
        <div class="class9_1"></div>
        <div class="class9_2"></div>
        <div class="class9_3"></div>
    </section>
    <section>
        <p>10.平行四边形</p>
        <div class="class10_1">
            <div>111111</div>
        </div>
        <div class="class10_2">
            <div>111111</div>
        </div>
    </section>
    <section>
        <p>11.菱形四边形</p>
        <div class="class11_1">
            <div>111111</div>
        </div>
        <div class="class11_2">
            <div>111111</div>
        </div>
    </section>
    <section>
        <p>12.切角特效</p>
        <div class="class12_1"></div>
        <div class="class12_2"></div>
    </section>
    <h1>视觉特色</h1>
    <section>
        <p>15.投影</p>
        <div class="class15"></div>
    </section>
    <section>
        <p>17.投影</p>
        <div class="class17"></div>
    </section>
    <section>
        <p>18.毛玻璃</p>
        <div class="class18"></div>
    </section>
    <section>
        <p>19.折角效果</p>
        <div class="class19"></div>
    </section>
    <h1>文字排版</h1>
    <section>
        <p>20.改变断行效果</p>
        <div class="class20">When you're down and &shy; out, remember to keep your head up. When you're up and well,
            remember to keep your feet down.</div>
    </section>
    <section>
        <p>21.文字效果展示</p>
        <div class="class21_1">text-shadow</div>
        <div class="class21_2">text-shadow</div>
        <div class="class21_3">css</div>
    </section>
    <section>
        <p>22.滚动效果💴</p>
        <div class="class22">
            <p>1</p>
            <p>2</p>
            <p>1</p>
            <p>2</p>
            <p>1</p>
            <p>2</p>
            <p>1</p>
            <p>2</p>
            <p>1</p>
            <p>2</p>
            <p>1</p>
            <p>2</p>
        </div>
    </section>
    <section>
        <p>23.打字效果</p>
        <div class="class23">Nothing worth doing in life is ever easy. If you want to do great work, it's going to take
            a lot of hard work to do it. </div>
    </section>
    <section>
        <p>24.缓动效果</p>
        <div class="class24_1">
            <div class="class24_2"></div>
        </div>
    </section>
    <section>
        <p>25.状态平衡动画</p>
        <div class="class25">
        </div>
    </section>
    <section>
        <div class="mouse"></div>
    </section>
</body>
<script>
    var oBox = document.getElementsByName('body');
    oBox.onmousedown = function (ev) {
        ev = ev || window.event;
        console.log(ev.offsetX, ev.offsetY);
        console.log(ev.clientX, ev.clientY);
        console.log(ev.pageX, ev.pageY);
        console.log(ev.screenX, ev.screenY);
        console.log(ev.layerX, ev.layerY);
    }
    var body = document.getElementsByTagName("body")[0];
    body.addEventListener('mousemove', function (ev) {
        console.log(ev.offsetX, ev.offsetY);
        var mouse = document.querySelector('.mouse');
        mouse.innerHTML = `<p>X坐标：${ev.offsetX}</p><p>Y坐标：${ev.offsetY}</p>`
    })
</script>

</html>
````
- css代码
````css
section {
  max-height: 300px;
  min-height: 80px; }

div {
  width: 100px;
  height: 100px; }

::selection {
  background: red; }

.class2_1, .class2_2, .class2_3, .class5_1, .class5_2, .class5_3, .class5_4, .class5_5, .class5_6, .class6_1, .class6_2, .class8_1, .class8_2, .class8_3, .class8_4,
.class9_1, .class9_2, .class9_3, .class10_1, .class10_2, .class11_1, .class11_2, .class12_1, .class12_2, .class21_1, .class21_3, .class21_2 {
  display: inline-block;
  margin: 10px; }

.mouse {
  position: fixed;
  right: 0;
  top: 0;
  z-index: 5;
  width: 100px;
  height: 100px; }

.class1 {
  position: absolute;
  cursor: pointer;
  background: red;
  height: 30px; }
  .class1:after {
    content: '';
    position: absolute;
    top: -5px;
    right: -5px;
    bottom: -5px;
    left: -5px; }

.class2_1 {
  background: #000;
  box-shadow: 0 10px #888, 10px 0px #786, -10px 0px #346, 0px -10px #821; }

.class2_2 {
  background: #000;
  box-shadow: inset 0 0 0 5px #888, 0 0 0 5px #786, 0 0 0 5px #346, 0 0 0 5px #821; }

.class2_3 {
  background: #000;
  outline: 10px solid #821;
  outline-offset: -10px; }

.class3 {
  background: url("../img/1.jpg") no-repeat top center red;
  background-position: 10px 20px;
  background-size: 20% 20%; }

.class4 {
  position: relative;
  cursor: pointer;
  padding: 10px;
  background: red;
  z-index: 1; }
  .class4:after {
    content: '';
    background: orange;
    position: absolute;
    top: 10px;
    right: 10px;
    bottom: 10px;
    left: 10px;
    z-index: -1;
    border-radius: 10px; }

.class5_1 {
  background: linear-gradient(red 50%, orange 50%);
  background-size: 100% 20%; }

.class5_2 {
  background: linear-gradient(134deg, red 50%, orange 50%);
  background-size: 100% 20%; }

.class5_3 {
  background: linear-gradient(to right, red 50%, orange 50%);
  background-size: 20% 100%; }

.class5_4 {
  background: linear-gradient(134deg, red 50%, orange 50%);
  background-size: 20% 100%; }

.class5_5 {
  background: linear-gradient(134deg, red 50%, orange 50%);
  background-size: 100% 20%; }

.class5_6 {
  background: linear-gradient(134deg, red 50%, orange 50%);
  background-size: 20% 20%; }

.class6_1 {
  background-image: linear-gradient(45deg, #897 30%, transparent 0), linear-gradient(45deg, transparent 75%, #897 0), linear-gradient(45deg, #897 25%, transparent 0), linear-gradient(45deg, transparent 75%, #897 0);
  background-size: 30% 30%; }

.class6_2 {
  background-image: linear-gradient(45deg, #297 30%, transparent 0), linear-gradient(to right, #297 30%, transparent 0), linear-gradient(75deg, #297 30%, transparent 0);
  background-size: 30% 30%; }

@keyframes col {
  20% {
    background: orange; }
  60% {
    background: #897; } }
@keyframes rad {
  50% {
    border-radius: 50%; } }
@keyframes zhuan {
  100% {
    transform: rotate(360deg); } }
.class7 {
  border: 10px solid red;
  background: #565;
  transform: .5s all;
  animation: col 2s infinite,rad 1s infinite,zhuan 1s infinite; }

.class8_1 {
  background: linear-gradient(white, white) padding-box, repeating-linear-gradient(-45deg, red 0, red 12.5%, transparent 0, transparent 25%, orange 0, orange 37.5%, transparent 0, transparent 50%) 0/5em 5em;
  border: 1em solid transparent; }

.class8_2 {
  background: linear-gradient(white, white) padding-box, repeating-linear-gradient(-45deg, red 0, red 12.5%, transparent 0, transparent 25%, orange 0, orange 37.5%, transparent 0, transparent 50%) 0/5em 5em;
  border: 1em solid transparent;
  animation: 2s zhan1 infinite; }

.class8_3 {
  border: 1em solid transparent;
  animation: 2s zhan1 infinite;
  background: linear-gradient(white, white) padding-box, repeating-linear-gradient(-45deg, black 0, black 25%, white 0, white 50%) 0/0.6em 0.6em; }

.class8_4 {
  border: 1px solid transparent;
  animation: 2s zhan1 infinite;
  background: linear-gradient(white, white) padding-box, repeating-linear-gradient(-45deg, black 0, black 25%, white 0, white 50%) 0/0.6em 0.6em; }

@keyframes zhan1 {
  100% {
    background-position: 100%; } }
.class9_1 {
  background: red;
  border-radius: 50px; }

.class9_2 {
  background: red;
  border-radius: 50%/100% 100% 0 0; }

.class9_3 {
  background: red;
  border-radius: 50%/100% 100% 0 50%; }

.class10_1 {
  transform: skew(45deg);
  background: red; }

.class10_1 > div {
  transform: skew(-45deg); }

.class10_2 {
  position: relative; }

.class10_2:before {
  content: "";
  position: absolute;
  top: 0px;
  right: 0px;
  bottom: 0px;
  left: 0px;
  z-index: -1;
  background: orange;
  transform: skew(45deg); }

.class11_1 {
  background: red;
  transform: rotate(45deg); }

.class11_1 > div {
  transform: rotate(-45deg); }

.class11_2 {
  background: orange;
  transform: rotate(45deg); }

.class11_2 {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
  transition: 1s clip-path; }

.class11_2:hover {
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%); }

.class12_1 {
  background: linear-gradient(45deg, transparent 20px, red 0); }

.class12_2 {
  background: radial-gradient(circle at top left, transparent 15px, red 0) top left, radial-gradient(circle at top right, transparent 15px, red 0) top right, radial-gradient(circle at bottom right, transparent 15px, red 0) bottom right, radial-gradient(circle at bottom left, transparent 15px, red 0) bottom left;
  background-repeat: no-repeat;
  background-size: 50% 50%; }

.class15 {
  background: orange;
  box-shadow: 0 5px 4px -4px black; }

.class17 {
  transition: 1.5s filter;
  filter: sepia(1) saturate(1) hue-rotate(295deg);
  background: red; }

.class17:hover {
  filter: none; }

.class18 {
  background: url(../img/1.jpg) no-repeat top center;
  background-size: 100%;
  filter: blur(2px); }

.class19 {
  background: blue;
  background: linear-gradient(to left bottom, transparent 50%, orange 0) no-repeat 100% 0/21px 21px, linear-gradient(-135deg, transparent 15px, red 0); }

.class20 {
  width: 300px;
  hyphens: auto; }

.class21_1 {
  color: #fff;
  background: red;
  text-shadow: 1px 1px black,-1px -1px black, 1px -1px black, -1px 1px black; }

.class21_2 {
  color: #fff;
  background: red;
  transform: .5s; }

.class21_2:hover {
  filter: blur(1px); }

.class21_3 {
  color: #fff;
  font-size: 34px;
  display: block;
  background: red;
  text-align: center;
  text-shadow: 0 1px #fbb7b7, 0 2px #f99f9f, 0 3px #f88787, 0 4px #f76e6e, 0 5px #f55656, 0 5px 10px black; }

.class22 {
  overflow-y: auto;
  background: url(../img/1.jpg) no-repeat;
  background-size: 50px 50px;
  background-position: 20% 30%;
  background-attachment: local,scroll; }

@keyframes typing {
  from {
    width: 0; } }
@keyframes caret {
  50% {
    border-right-color: transparent; } }
.class23 {
  max-width: 100%;
  width: 800px;
  height: 25px;
  white-space: nowrap;
  overflow: hidden;
  border-right: .05em solid;
  animation: typing 8s steps(100) infinite, caret 2s steps(1) infinite; }

.class24_1 {
  background: green;
  position: relative; }

.class24_2 {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: red;
  position: relative;
  animation: bounce 6s infinite; }

@keyframes bounce {
  60%,
    80%,
    to {
    transform: translateY(40px);
    animation-timing-function: ease; }
  70% {
    transform: translateY(50px); }
  90% {
    transform: translateY(60px); } }
@keyframes bk1 {
  20% {
    background-position: 100% 100%; }
  40% {
    background-position: 0% 100%; }
  60% {
    background-position: 100% 0%; } }
.class25 {
  background: url(../img/1.jpg);
  animation: bk1 10s infinite;
  animation-play-state: paused; }

.class25:hover {
  animation-play-state: running; }
````