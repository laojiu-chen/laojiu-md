#css3中 2D 3D动画效果
##css3 2D转换

**CSS3 转换就是对元素进行移动、缩放、转动、拉长或拉伸。**

**1. translate() 方法** 
    *translate()方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动*
```
transform: translate(50px,100px);

transform: translateX(50px);

transform: translateY(100px);
```
**应用translate水平垂直居中**
 + translate通过位移，可以不用担心元素脱标的情况，会占位
 + 使用translate实现盒子的水平垂直居中对齐：
   ```
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    ```
  

**2. rotate() 方法**
*rotate()方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。2D旋转是绕着z轴旋转。<font style="color:red">注意：旋转中心是盒子的正中心，可以使transform-origin属性改变盒子的旋转中心点</font>*

```
transform: rotate(30deg);

transform-origin：left top;  //将旋转中心设置为盒子左上角，left和top之间别加逗号要不然无效
```

**3.scale() 方法**
*scale()方法，该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数：*

```
transform: scale(2,3);  //放大盒子的宽两倍和高三倍

transform: scale(2);    //放大盒子的宽高laingbei
```

**4.skew() 方法**
*分别表示X轴和Y轴倾斜的角度，如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜*

<font style="color:red">和rotate区别：
1.会改变盒子形状，skew 的两个 deg 参数互不影响，but，当其中之一改变时，目标的形状亦会随之改变，
2.当skew的两个值一同改变相同值，实际上就是将该盒子rotate那个值，并放大若干倍
</font>
```
transform: skew(30deg,30deg);

transform: skewX(30deg);

transform: skewY(30deg);
```
**5.matrix() 方法**
*matrix()方法就是将2D变换方法合并成一个。
matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。*
```
transform:matrix(0.866,0.5,-0.5,0.866,0,0);
```

##CSS3 3D 转换
3D是在2D的基础之上加上了z轴，加上perspective属性让图形实现近大远小的效果

**转换属性**

|属性|描述|CSS|
|---|---|---|
|transform|实现3D效果|3|
|transform-origin|允许你改变被转换元素的旋转中心位置|3|
|transform-style|规定被嵌套元素如何在 3D 空间中显示。|3|
|perspective|规定 3D 元素的透视效果。|3|
|perspective-origin|规定 3D 元素的底部位置。|3|
|backface-visibility|定义元素在不面对屏幕时是否可见。|3|

 *1.perspective属性的理解：perspective是人观察图像的视距，当视距越小被观察的图像就会看起来越大，但perspective的值不能小于translateZ的值，小于后图像将会观察不到。*
 
 *2.transform-style用于显示图片的3D效果，让图形看起来和真实现实世界效果一样，<font style="color:red">注意要让子盒子显示效果，必须给父盒子设置transform-style</font>

##css3 过渡
*CSS3中，我们为了添加某种效果可以从一种样式转变到另一个的时候，无需使用Flash动画或JavaScript。*
**使用方法**
+ 指定要添加效果的CSS属性
+ 指定效果的持续时间。
```
    transition: width 2s;

    transition: width 2s, height 2s, transform 2s; //多项属性发生改变

    transition: all 1s;    //多项属性发生改变

```
**过渡属性**

|属性|描述|CSS|
|---|---|---|
|transition|简写属性，用于在一个属性中设置四个过渡属性。|3|
|transition-property|规定应用过渡的 CSS 属性的名称。|3|
|transition-duration|定义过渡效果花费的时间。默认是0|3|
|transition-timing-function|规定过渡效果的时间曲线。默认是 "ease"。|3|
|transition-delay|规定过渡效果何时开始。默认是 0。|3|

##CSS3 动画
css3使用规则当在 @keyframes 创建动画，把它绑定到一个选择器，否则动画不会有任何效果。指定至少这两个CSS3的动画属性绑定向一个选择器：

+ 规定动画的名称
+ 规定动画的时长

实例：
```
@keyframes myfirst
{
    0%   {background: red;}
    25%  {background: yellow;}
    50%  {background: blue;}
    100% {background: green;}
}
 
 ```
|属性|描述|CSS|
|---|---|---|
|@keyframes|规定动画。|3|
|animation|所有动画属性的简写属性，除了 animation-play-state 属性。|3|
|animation-name|规定 @keyframes 动画的名称。|3|
|animation-duration|规定动画完成一个周期所花费的秒或毫秒。默认是 0。|3|
|animation-timing-function|规定动画的速度曲线。默认是 "ease"。|3|
|animation-fill-mode|规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。|3|
|animation-delay|规定动画何时开始。默认是 0。|3|
|animation-iteration-count|规定动画被播放的次数。默认是 1。|3|
|animation-direction|规定动画是否在下一周期逆向地播放。默认是 "normal"。|3|
|animation-play-state|规定动画是否正在运行或暂停。默认是 "running"。|3|


*补充 steps 用于描述动画的步长也就是动画的帧数，默认是会忽略最后一帧。而且动画时间是不能省的*
实列：
```
animation: rotate[名称] 3s[时间] steps(10)[步长];
```