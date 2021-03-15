狂神CSS参考笔记

https://blog.csdn.net/pan_h1995/article/details/105827181

# 基本选择器：

id，类，标签

# 层次选择器

1后代选择器 示例中指的是body下的p标签的背景颜色都为红色

```css
body p{
  background: red;
}
```

2子选择器 示例中指的是body的子标签p的颜色设置为红色

```css
body > p{
  color:red;
}
```

3相邻兄弟选择器 **相邻兄弟选择器（Adjacent sibling selector）可选择紧接在另一元素后的元素，且二者有相同父元素。如果需要选择紧接在另一个元素后的元素，而且二者有相同的父元素，可以使用相邻兄弟选择器（Adjacent sibling selector）。**

https://www.cnblogs.com/hanmk/p/9062084.html

4通用兄弟选择器 它是用来指定位于同一个父元素之中的某个元素之后的所有其他某个种类的兄弟元素所使用的样式。

https://blog.csdn.net/u012859748/article/details/52612396

#  结构伪类选择器

https://www.cnblogs.com/yanggeng/p/11188285.html

ul下第一个li

```css
/*ul下第一个li*/
ul li:first-child{
  background: green;
}
/*ul下最后一个li*/
ul li:last-child{
  background: red;
}
```

选中当前p元素的父级元素，选中后父级的第一个子元素（如果父级的第一个子元素不是p的话，则样式不会生效）

```html
<style>
  p:nth-child(1){
    background: green;
  }
</style>
<body>
<p>p1</p>
<p>p2</p>
<p>p3</p>
<ul>
  <li>li1</li>
  <li>li2</li>
  <li>li3</li>
</ul>
</body>
```

选中当前p元素的父级元素，选中后父级的第二个p

```css

p:nth-of-type(2){
  background: green;
}
```

# 属性选择器

=是绝对等于
	*=包含
	^=以这个开头
	$=以这个结尾	
        /*a里存在id元素的a标签*/
        a[id]{
            background-color: red;
        }
        /*a里存在id  = first元素的a标签*/
        a[id = first]{
            background-color: #2c3e50;
        }
        /*a里id里有first元素的a标签*/
        a[class *= first]{
            background-color: rebeccapurple;
        }
        /*a里href里有http开头元素的a标签*/
        a[href ^= http]{
            color: red;
        }
        /*a里href里有pdf结尾元素的a标签*/
        a[href $=pdf]{
            color: black;
        }
    ``<a href="http://www.baidu.com" class="links item first" id="first">1</a>`
    `<a href="" class="links item active" target="_blank" title="test">2</a>`
    `<a href="./imgs/123.html" class="links item">3</a>`
    `<a href="./imgs/123.png" class="links item">4</a>`
    `<a href="./imgs/123.jpg" class="links item">5</a>`
    `<a href="abc" class="links item">6</a>`
    `<a href="a.pdf" class="links item">7</a>`
    `<a href="/abc.pdf" class="links item">8</a>`
    `<a href="abc.doc" class="links item">9</a>`
    `<a href="abcd.doc" class="links item last">10</a>``

字体属性
            font-family: "Agency FB";
            font-size: medium;
            font-weight: bold;

颜色
color: #000000 到#FFFFFF

rgb：0-F
color: rgb(0,255,255)
rgba增加了一个参数透明度 透明度一般为0~1
color: rgb(0,255,255,0.5)


对齐方式
 img 和src居中对齐

 img,span{
            vertical-align: middle;
 }

    /*鼠标放在连接上的颜色*/
        a:hover{
            color: orange;
            font-weight: bold;
            font-size: 50px;
        }
        /*鼠标按住未释放的样式*/
        a:active{
            color: green;
        }
        /*链接点完之后的样式*/
        a:visited{
            color:#00FF00
        }
        /*设置文本阴影*/
        .price{
            text-shadow: 10px 10px 2px #3cc7f5;
        }
列表 
/*去除列表的样式*/
list-style: none;
背景
/*可以给div设置背景图片 默认是吧图片铺满整个div*/
 background-image: url("imgs/1.png");
/*水平平铺*/
 background-repeat: repeat-x;
/*第一个参数为颜色 距离左边的宽度 距离上边的宽度  设置不重复*/
background: red url("imgs/1.png") 200px 10px no-repeat;
/*相当于*/
background-color
background-image
background-position
background-repeat

渐变
https://www.grabient.com

4盒子模型

# 前台模板

源码之家

XXX 模板之家

飞冰



