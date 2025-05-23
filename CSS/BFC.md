## 什么是BFC
BFC,全称`Block Formatting Context`,块级格式上下文；是一种特殊的块级上下文。当触发了BFC之后，BFC内的任何元素都不会影响到BFC外，同样的，BFC外的元素也不会影响到BFC内

## BFC的作用
1. 防止父元素出现`margin塌陷`:下面代码如果不启用overflow，那么会变成container距离窗口100px，而不是box距离container有100px
```css
.container{
    height:300px;
    width:300px;
    background-color:blue;
    /* overflow:hidden; */
}
.box{
    background:red;
    height:100px;
    width:100px;
    margin-top:50px;
}
```

```html
<div class="container">
    <div class="box">
    </div>
</div>
```

2. 避免外边距的margin合并（当两个兄弟元素有margin-left:100px和margin-right:100px的时候，如果不具有BFC属性，那么实际渲染的间距只有100px）
3. 清除子元素的浮动
下方代码如果不启用overflow，那么就会变成2px高的线条和它下方的红色方块
```css
.container{
    border:1px solid;
    /* overflow:hidden; */
}
.box{
    background:red;
    height:100px;
    width:100px;
    float:left;
}
```

```html
<div class="container">
    <div class="box">
    </div>
</div>
```

## 触发BFC的方法
1. `overflow` 选择 `visible` 之外的值  
2. `float` 不为 `none`  
3. `position` 选择 `absolute` / `fixed`  
4. `display` 选择 `inline-block`、`flex`、`inline-flex`、`grid`、`inline-grid`、`flow-root`