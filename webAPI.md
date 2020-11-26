##webAPI
web API的概念:是浏览器提供的一套操作浏览器功能和页面元素的 API ( BOM 和 DOM )。

###DMO
####  DOM树
![DOM树形图](img/DOMshu.png)
DOM树 又称为文档树模型，把文档映射成树形结构，通过节点对象对其处理，处理的结果可以加入到当前的页面。

- 文档：一个页面就是一个文档，DOM中使用document表示
- 节点：网页中的所有内容，在文档树中都是节点（标签、属性、文本、注释等），使用node表示
- 标签节点：网页中的所有标签，通常称为元素节点，又简称为“元素”，使用element表示
####  获取元素
document.getElementById("id");
document.getElementsByClassName("类名")
document.getElementsByTagName('标签名')
用TagName和ByClassName接受元素返回的是一个伪数组，用下标来得到具体的元素如：
```
var lis = document.getElementsByTagName('li');
lis[0];           //这是第一个"li"元素
```
**H5新增的获取元素的方法**
document.querySelector('选择器') (有ID选择器、类名选择器、标签选择器)
document.querySelectorAll('选择器') (同上)
用querySelectAll()接受元素返回的是一个伪数组和Tag Name()一样。

**两个特殊的对象**
body对象： document.body
html对象： document.documentElement

#### 事件基础
        事件的三要素：事件源，事件类型，事件处理函数

        语法：事件源(dom对象).事件类型 = 事件处理函数
常见的鼠标事件：
![常用鼠标事件](img/mouseEvent.png)
```
var btn = document.querySelector("button");
button.onclick = function () {
    事务处理
}
```
#### 操作元素（属性）

      (1)获取属性
        固有属性：   1. node.属性名   2.node.getAttribute(属性名)
        自定义属性： 1.node.getAttribute(属性名)
          规范：data-开头:   node.dataset.[没有data-的属性名] ：div.dataset.type
                  
      (2)修改属性值
        固有属性：   node.属性名 = xxxx
        固有属性与自定义属性：node.setAttribue(属性名,属性值)

#### 节点查找
      1.查找找节点
        父节点：node.parentNode
        
        子节点：node.children
          找第一个儿子：node.children[0]
          找最后一个儿子：node.children[node.children.length-1]

        兄弟节点：
          找哥哥：previousElementSibling
          找弟弟：nextElementSibling

      2.创建节点
        document.createElement(标签名称)
        
      3.节点的追加
        父节点.appendChild(子节点)            父节点添加了最后一个子节点
        父节点.insertBefore(子节点,位置节点)   父节点根据位置节点插入节点

      4.节点的删除  
        父节点.removeChild(子节点)   父杀子
        节点.remove()  自杀

      5.节点的复制
        节点.cloneNode()       只复制节点,不复制内容
        节点.cloneNode(true)   即复制节点,又复制内容
####  f.事件高级
      1.事件绑定的两种方式：
        事件源.事件类型 = 事件处理函数
        事件源.addEventListener("事件类型",function(){},useCapture[fasle])
 <font style="color: red;">useCapture就是捕获和冒泡所用到的属性，默认是fasle为捕获</font>

      2.事件解绑
        事件源.事件类型 = null
        事件源.removeEventListener("事件类型",function(){})

      3.事件流
        冒泡 与 捕获
![1551166555833](img/EventFlow.png)
      4.事件对象：event
        记录了当次事件的一些信息

      5.目标对象event.target与this的区别

        -  this 是事件绑定的元素（绑定这个事件处理函数的元素） 。

        -  e.target 是事件触发的元素。

      6.阻止事件默认行为
        event.preventDefault()

      7.阻止事件冒泡
        event.stopPropagation()
      
      8.事件委托
        原理:事件冒泡
        好处:动态添加的元素也能绑定事件(将事件绑定到父级元素上)

      9.获取鼠标在页面上的坐标信息
        可视区坐标
          e.clientX
          e.clientY
        文档坐标
          e.pageX
          e.pageY
        屏幕坐标
          e.screenX
          e.screenY

      10.常见的键盘事件
         onkeydown  : 键盘按下
         onkeyup : 键盘抬起
         onkeypress: 键盘按下  不识别功能键

         event.keyCode (鼠标的ASCLL码)

### 2.BOM  browser object model  浏览器对象模型
  #### window对象

  1.注意点:
    在全局作用域下,声明一个变量,相当于给window对象添加了一个属性
    在全局作用域下,声明一个函数,相当于给window对象添加了一个方法
  
  2.window是顶级对象,它有很多的儿子
    document文档  location地址栏  history历史记录  navigator导航  screen屏幕对象 ...
#### window的基本事件
  事件:
      (a) window.onload = function(){} 
        当页面元素及 "资源" 全部加载完毕时,才执行这个事件

        与window.onload相像的一个事件 document.addEventListener("DOMContentLoaded",function(){})
        当页面元素全部加载完毕时,才执行这个事件

      (b) window.onresize = function(){}  
        当浏览器的窗口大小改变时触发

  属性: 
    name  
    innerWidth
    innerHeight

  方法: 
    alert()   警式框
    prompt()  输入框
    confirm() 确认框

    setTimeout()  延时器
      语法:
        var timer = window.setTimeout(function(){},毫秒)

    clearTimeout(timeID)  清除延时器
      语法:
        clearTimeout(timer)

    setInterval() 定时器 
      语法:
        var timer = window.setInterval(function(){},毫秒)

    clearInterval(timeID)  清除定时器
      语法:
        var timer = window.clearInterval(timer)

  #### window对象的子对象location
    (a) location地址栏对象 如:https://www.baidu.com/xxx.html?name=jack#link
      属性:
        herf:完整的路径  "http://www.baidu.com/xxx.html?name=jack"
        serach:参数      "?name=jack"
        protocol:协议    "https"
        hash: 锚点       "#link"
        ...

        location.href = "xxxx" 赋值并跳转
      方法:
        assign()   相当于 location.href="xxx"中的赋值操作
        replace()  也是地址栏赋值,但是没有历史记录
        reload()   刷新

    (b)历史记录对象history
       方法:
         forward()  前进
         back()   后退
         go(2)

    (c)navigator导航
#### 事件队列和同步与异步

  a.同步与异步
    同步: 有多个任务, 一个任务接一个任务的完成
    异步: 有多个任务, 在同一时间可以执行多个任务

    Javascript是一门运行在客户端,面向对象的,事件驱动,(单线程加事件队列)的一门编程语言。

  b.js的执行机制(非常重要)
    前端js中哪些是属于事件队列的
        1.setTimeout  setInterval
        2.所有以on开头的事件 onclick onblur onfocus ...
        3.ajax中 onreadystatechange

    事件队列中的代码执行的条件
    前提条件:所有的主线程中的代码都执行完毕
        1.时间到了
        2.事件触发了
        3.数据从服务器端返回了

#### 本地存储
  sessionStorage:
    a.存储的大小：5M 
    b.生命周期：销毁关闭浏览器的窗口
    c.存储的格式：健值对  重点：值一定是一个字符串
  localStorage:
    a.存储的大小：20M     
    b.生命周期：永久存储
    c.存储的格式：健值对  重点：值一定是一个字符串
    d.数据共享:多窗口可以共享同一个数据,但是是在同一个域名下才能共享数据
   
  常见的方法：
    存:setItem(健，值)
    查:getItem(健)
    删:removeItem(健)
        clear()清空

### 其他位置属性与方法

  a.offset系列
    offsetParent: 返回带有定位的父级元素，如果都没有定位，返回body元素
    offsetTop: 返回带有定位父级元素的上偏移量
    offsetLeft:返回带有定位父级元素的左偏移量
    offsetWidth:  元素的宽(包括padding与border)  content+padding+border
    offsetHeight: 元素的高(包括padding与border)  content+padding+border
    
    style: 用来设置元素的样式   node.style.xxxx 
    offset:用来读取元素的样式   node.offsetWidth

  b.client系列
    clientTop: 返回上边框的宽度
    clientLeft:返回左边框的宽度
    clientWidth:  元素的宽(包括padding，不含border)  content+padding
    clientHeight: 元素的高(包括padding，不含border)  content+padding

  c.scroll系列
    scrollTop: 返回向上滚动的高度
    scrollLeft:返回向左滚动的宽度
    scrollWidth:  元素内容实际的宽度
    scrollHeight: 元素内容实际的高度
    
    获取点击的对象：e.targer
    获取点击的对象的位置为：e.pageX，e.pageY;
    
#### 移动端常见事件
    touchstart: 开始触摸
    touchmove: 按下持续触摸
    touchend: 结束触摸

    事件对象中手指信息
    e.touches : 记录了当前屏幕上的所有手指信息
    e.targetTouches : 记录了当前元素上的所有手指信息 
    e.changedTouches : 记录了元素上的手指信息的改变 (从有到无 从无到有)


