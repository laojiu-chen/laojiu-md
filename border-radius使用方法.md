#border-radius使用
border-radius的数值有三种表示方法：px、%、em，对于border-radius的值的设置，我们常用的有三种写法：
## 1. 使用px表示数值的情况
border-radius后面接的数值改变边框的圆角成度，数值从小到大改变边框的圆角成度也随着改变的越大当改变的数值达到这个盒子的长宽的一半时盒子将变成一个圆.原理就是将圆弧的一部分替代边框一部分。
![avatar](/img/border-radius1.png)
## 2. 使用%表示数值的情况
使用%来表示圆角值的时候，如果对象的宽和高是一样的，那判断方法与第一点一致，只不过想象的时候，需要将宽高乘以百分数换算一下；

如果宽高不一致，那产生的效果，其实就是以对象的宽高乘以百分数后得到的值r1和r2，作为两条半径绘制出来的椭圆产生的弧度。
![avatar](/img/border-radius2.png)

##需要注意的情况
在设置对象为圆形的时候，如果使用了border、padding等情况时，对象的实际显示宽高已经不再是设置的width和height的数值，如果border-radius设置的值仍为原本的width和height的一半，可能达不到预期的真正的圆形的效果。

　　如下面这个例子，给div加了10px的边框，但是border-radius仍是以100px的一半来设置的，显示出来的效果显然就不是一个真正的圆形。
![avtar](/img/border-radius3.png)
可以通过设置百分比50%的方式来解决这一情况，或者计算一下实际的高度再来设置border-radius的数值。上面这个例子，div实际的宽高应该是100 + 10 * 2 = 120px，所以border-radius应该设置为60px。
![avtar](/img/border-radius4.png)
## 3. border-radius完整结构形式
在W3C上查border-radius属性时，会发现上面描述的语法是这样的：

　　　　　　border-radius: 1-4 length|% / 1-4 length|%;
 　这是border-radius的完整写法，我们平时的写法其实都是简写，平时我们写的border-radius : 50px，其实完整的写法应该是：

　　　　border-radius : 50px 50px 50px 50px / 50px 50px 50px 50px;

 　　“/”前的四个数值表示圆角的水平半径，后面四个值表示圆角的垂直半径，什么是水平半径和垂直半径呢，见下图:
 ![avtar](/img/border-radius5.png)