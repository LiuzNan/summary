### 第1天

##### 【html】页面导入样式时，使用link和@import有什么区别？

```
区别：
1.link是html标签，除了加载css外，还可以定义RSS等其他事务；@import属于css范畴，只能加载css
2.link引入的样式页面加载时同时加载；@import引入的样式需要页面加载完成后再进行加载
3.link是html标签，没有兼容性问题；@import是css2.1提出的，不支持低版本浏览器
4.link可以通过js操作DOM去改变样式；@import不支持
```

##### 【css】圣杯布局和双飞翼布局的理解和区别，并用代码实现

```html
作用：
圣杯布局和双飞翼布局都是解决两边定宽，中间自适应的三栏布局解决方案，中间栏放在文档流前面 让浏览器自上而下优先渲染。
区别：
圣杯布局，为了中间 div 内容不被遮挡，将中间 div 设置 padding-left 和 padding-right 后，将左右两个 div 用相对布局 position: relative 并分配 right 和 left 属性，以便左右两栏 div 移动后不遮挡中间 div
<body>
<div id="hd">header</div>
<div id="bd">
  <div id="middle">middle</div>
  <div id="left">left</div>
  <div id="right">right</div>
</div>
<div id="footer">footer</div>
</body>

<style>
#hd{
    height:50px;
    background: #666;
    text-align: center;
}
#bd{
    /*左右栏通过添加负的margin放到正确的位置了，此段代码是为了摆正中间栏的位置*/
    padding:0 200px 0 180px;
    height:100px;
}
#middle{
    float:left;
    width:100%;/*左栏上去到第一行*/
    height:100px;
    background:blue;
}
#left{
    float:left;
    width:180px;
    height:100px;
    margin-left:-100%;
    background:#0c9;
    /*中间栏的位置摆正之后，左栏的位置也相应右移，通过相对定位的left恢复到正确位置*/
    position:relative;
    left:-180px;
}
#right{
    float:left;
    width:200px;
    height:100px;
    margin-left:-200px;
    background:#0c9;
    /*中间栏的位置摆正之后，右栏的位置也相应左移，通过相对定位的right恢复到正确位置*/
    position:relative;
    right:-200px;
}
#footer{
    height:50px;
    background: #666;
    text-align: center;
}
</style>

双飞翼布局，为了中间 div 内容不被遮挡，直接在中间 div 内部创建子 div 用于放置内容，在该子 div 里用 margin-left 和margin-right 为左右两栏 div 留出位置
<body>
<div id="hd">header</div> 
  <div id="middle">
    <div id="inside">middle</div>
  </div>
  <div id="left">left</div>
  <div id="right">right</div>
  <div id="footer">footer</div>
</body>

<style>
#hd{
    height:50px;
    background: #666;
    text-align: center;
}
#middle{
    float:left;
    width:100%;/*左栏上去到第一行*/     
    height:100px;
    background:blue;
}
#left{
    float:left;
    width:180px;
    height:100px;
    margin-left:-100%;
    background:#0c9;
}
#right{
    float:left;
    width:200px;
    height:100px;
    margin-left:-200px;
    background:#0c9;
}

/*给内部div添加margin，把内容放到中间栏，其实整个背景还是100%*/ 
#inside{
    margin:0 200px 0 180px;
    height:100px;
}
#footer{  
   clear:both; /*记得清楚浮动*/  
   height:50px;     
   background: #666;    
   text-align: center; 
} 
</style>
```

##### 【js】用递归算法实现，数组长度为5且元素的随机数在2 - 32之间不重复的值

```javascript
function buildArray(arr, length, min, max) {
    var num = Math.floor(Math.random() * (max - min + 1)) + min;
    if (!arr.includes(num)) { arr.push(num); }
    return arr.length === length ? arr : buildArray(arr, length, min, max);
}
var result = buildArray([], 5, 2, 32);
console.table(result);
```

### 第2天

##### 【html】html的元素有哪些（包含h5）？

```
行内元素：a、b、span、img、input、strong、select、label、em、button、textarea
块级元素：div、ul、li、dl、dt、dd、p、h1-h6、blockquote
空元素:br、meta、hr、link、input、img
H5新增元素：section、article、audio、video、hearder、footer、small、canvas
```

##### 【css】css3有哪些新增特性？

```
边框圆角：border-radius
盒子阴影：box-shadow
文字阴影：text-shadow
边框背景：border-image
过渡：transition
动画：animation
转换：transform
线性渐变：linear-gradient
径向渐变：radial-gradient
倒影：box-reflect
弹性盒子：flexbox
媒体查询：@media
```

##### 【js】写一个方法去掉字符串中的空格

```javascript
function trimStr(str, type) {
    const regObj = {
        left: /^\s+/,
        middle: /(^\s+)(\S)|\s+(\S)/g,
        right: /\s+$/,
        both: /(^\s+)|(\s+$)/g,
        all: /\s+/g
    };
    const reg = type && regObj[type] ? regObj[type] : regObj.both;
    const replaceStr = type === 'middle' ? (m, $1, $2, $3) => $1 ? m : $3 : '';
    return str.replace(reg, replaceStr);
}
trimStr('  aa bb  cc d d ee  ','middle');
```

### 第3天

##### 【html】html全局属性（Global attribute）有哪些（包含h5）？

```
accesskey:设置快捷键
class:为元素设置类标识
contenteditable:指定元素内容是否可编辑
contextmenu:自定义鼠标右键弹出上下文菜单内容（仅firefox支持）
data-*:为元素增加自定义属性
dir：设置元素文本方向（默认ltr；rtl）
draggable:设置元素是否可拖拽
dropzone:设置元素拖放类型（copy|move|link,H5新属性，主流均不支持）
hidden:规定元素仍未或不在相关
id:元素id，文档内唯一
lang:元素内容的语言
spellcheck:是否启动拼写和语法检查
style:行内css样式
tabindex:设置元素可以获得焦点，通过tab导航
title:规定元素有关的额外信息
translate:元素和子孙节点内容是否需要本地化（均不支持）
```

##### 【css】在页面上隐藏元素的方法有哪些？

```
占位：
visilibity: hidden
margin-left: -100%
opacity: 0
transform: scale(0)
不占位：
display: none
overflow: hidden
```

##### 【js】去除字符串中最后一个指定的字符

```javascript
function delLast(str,target) {
  let reg =new RegExp(`${target}(?=([^${target}]*)$)`)
  return str.replace(reg,'')
}
let str = delLast('abbcdddfee', 'e')
console.log(str)
```

