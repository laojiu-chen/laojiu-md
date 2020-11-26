## 语义化标签

- header
- footer
- section（块）
- aside（侧边栏）
- nav（导航）

```html
<nav>
    <a href="##">新闻</a>
    <a href="##">新闻</a>
</nav>
```

**注意：**为了兼容低版本的浏览器，一般会在初始化样式的时候，加下面代码：

```css
header, footer, aside {
    display: block;
}
```

## 多媒体标签

### video

```html
<video src="test.mp4" controls></video>
```

- controls（播放控件）
- autoplay（自动播放），一般都是配合 muted 使用
- muted（静音）
- loop（循环播放）
- poster（记载前的图片预览）

### audio

```html
<audio controls>
    <source src="happy.mp3" type="audio/mpeg" >
    <source src="happy.ogg" type="audio/ogg" >
</audio>
```

## 新增的表单元素及属性

### 新增元素

- number（数字）
- email
- tel（移动端会用）
- search
- time
- color

```html
<!-- 测试的时候要包在 form 里面，并且要是 submit 按钮 -->
<form>
    <input type="tel" required/>
    <input type="submit" value="提交"/>
<form>
```

### 对应的一些属性

- placeholder（仅仅用来提示而已，和value不一样）
- required（必填）
- autofocus（自动获取焦点）
- maxlength（最大长度）

## 新增选择器

### 属性选择器

- div[title]，选择div，并且这个div有title属性
- div[title="你好"]，选择div，并且这个div的title属性是"你好"
- div[title^="你好"]，选择div，并且这个div的title属性是"你好"开头的
- div[title$="你好"]，选择div，并且这个div的title属性是"你好"结尾的
- div[title*="你好"]，选择div，并且这个div的title属性包含"你好"两个字

### 结构伪类选择器

- ul li:first-child
- ul li:nth-child(n)，n 是从 0 开始的
- ul li:nth-child(3)，n 支持数字，找 ul 里面的第三个子元素，并且这个子元素是 li
- ul li:nth-of-type(3)，先找 ul 下的 li，把同类的li筛选出来，然后从这里面再找第三个

- ul li:nth-child(-n+5)，前 5 个，包括第5个
- ul li:nth-child(n+5)，从第 5 个开始，包括第5个，后面的元素

### 伪元素选择器

```css
/* 往div的内容的最后加东西，一定要配合 content 使用 */
div::after {
    content: "";
}
```

- 应用场景：字体图标、替代一些空标签、清除浮动

## CSS3新增

- filter: blur(15px); 实现模糊
- CSS3 盒模型

```css
/* 最终宽度的计算包括 padding 和 border */
div {
    box-sizing: border-box;
    width: 100px;
    padding: 10px;
    border: 5px;
}
```

- `transition: 过渡的属性 动画执行的事件 动画的执行效果 延迟多久执行`，注意在做过度时要加起始值，谁做过渡给谁加

```css
div {
    transition: 1s;
}
```

## 使用 CSS，自行查找如何使网站变灰