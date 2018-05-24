## 图片+文字块内垂直居中

父用**display:table-cell**，父子用 **vertical-align: middle**

```CSS
.main{
	width: 500px;
  height: 70px;
  border: 1px solid black;
  vertical-align: middle;
  display: table-cell;
}
img{
  width: 50px;
 	height: 50px;
  vertical-align: middle;
}
```

父用 **height = line-height** 父子用 **vertical-align: middle**
```css
.main{
    width: 500px;
    height: 170px;
    border: 1px solid black;
    line-height: 170px;
    vertical-align:middle;
}
img{
    width: 50px;
    height: 50px;
    vertical-align:middle;
}
```



## 元素垂直居中

用`transform: translate(-50%,-50%);`代替margin

```CSS
.main{
  width: 500px;
  height: 70px;
  border: 1px solid black;
  position: relative;
}
img{
	width: 50px;
  height: 50px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%);
  /*transform: translate(-50%,-50%);*/
}
```

**flex**布局

```css
.main{
    width: 500px;
    height: 170px;
    border: 1px solid black;
    display:flex;
    display: -webkit-flex; 	/* Safari */
    align-items:center;			/*指定垂直居中*/
}
img{
    width: 50px;
    height: 50px;
}
```

## 图片响应式自适应

```css
.heade-bg {
  width: 100%;
  height: auto;
}
```

