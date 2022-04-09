# 1.为什么块级元素能够通过`margin:0 auto`实现水平居中，却不能实现垂直居中

```css
块级元素设置居中的前提是设置了width，若在css中没写width则会默认占据100%的宽度。auto指平分剩余空间 比如上图中父div宽度为200px，子div宽度为100px,则水平方向平分剩余宽度为(200-100)/2

#parent{
	height: 200px;
	width: 200px;
	background: black;
	margin: 0 auto;
}
#child{
	height: 100px;
	width: 100px;
	background: red;
	margin: 0 auto;
}
为什么margin:auto不能实现在垂直方向上的居中呢？ 因为默认垂直方向上没有剩余空间 如果子元素设置了绝对定位且四边都设为0，子元素会填充整个父元素的所有剩余空间，auto就能平均分配水平和垂直方向的剩余空间了。
```



当元素不存在width属性或者（width：auto）的时候，负margin会增加元素的宽度

注意：
margin-top为负值不会增加高度，只会产生向上位移
margin-bottom为负值不会产生位移，会减少自身的供css读取的高度



# CSS经典布局

* 单列布局1 header,content和footer等宽的单列布局

* 单列布局2 header与footer等宽,content略窄的单列布局

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/11/7/166ed4e13cc2753f~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

# CSS盒子模型

> 盒子模型分为IE盒子 W3C盒子
>
> W3C标准盒子模型  属性heigth，witdh只包含content，不包含border和padding
>
> IE盒子模型  属性width，height包含border和padding
>
> 在IE8浏览器及以上使用哪个盒子模型可以由box-sizing控制，默认值是content-box，即标准盒子模型，可以使用border-box设置为IE盒子模型
>
> #### content-box（标准盒模型）
>
> #### width = 内容的宽度
>
> #### height = 内容的高度
>
> #### border-box（IE盒模型）
>
> #### width = border + padding + 内容的宽度
>
> #### height = border + padding + 内容的高度
>
> ```css
> .box {
>     width:200px;
>     height:200px;
>     background-color:pink;
>     box-sizing: border-box; // 此时内容宽高为 160px 160px 减去了border和padding，注意margin和本身的宽高无关
>     border: 10px solid;
>     padding: 10px;
> }
> ```
>
> 盒子模型下上边距和下边距会发生合并，demo1和demo2都是div元素，他们的上下间距是20px而不是30px
>
> ```css
>  .demo1 {
>         width: 40px;
>         height: 40px;
>         background: pink;
>         padding: 10px;
>         margin: 10px 0px;
>         border: 2px solid pink;
>     }
>     .demo2 {
>         width: 40px;
>         height: 40px;
>         padding: 10px;
>         background: blue;
>         margin: 20px 0px;
>         border: 2px solid blue;
>     }
> ```
>
> `boder-box`用来解决什么问题？
>
> border-box的诞生，主要就是解决content-box的最大缺点。border-box意味着子容器的padding和border的厚度都算在50%之内，这样，你可以随意的修改padding和border的厚度值，根本不用担心父容器被撑爆。因此border-box使用场景如下:
>
> 子元素有padding和border，或者至少有其一，并且需要给子元素设定100%宽度（或者50%宽度等等），这时候显然需要border-box。设为border-box之后，padding和border的厚度可以随意调，并不会溢出父元素。如果是content-box，那么，宽度必然会溢出，而且，为了不溢出，你设定子元素的宽度就只能是一个定值，或者是一个计算值（比如calc(100% - 20px)。下面是两个div各占一半的写法
>
> ```css
> .demo1 {
>     width: 50%;
>     background-color: #8CC7B5;
>     height: 200px;
>     padding: 0 50px;
>     box-sizing: border-box;
>     margin: 0;
> 
> }
> .demo2 {
>     width: 50%;
>     background-color: #D1BA74;
>     height: 200px;
>     padding: 0 50px;
>     box-sizing: border-box;
>     margin: 0;
> }
> ```

# offsetLeft、offsetWidth、clientWidth、scrollWidth、style.width

> * `offsetLeft和offsetTop`
>
> 这两个都是**只读属性**。offsetLeft从字面意思上理解，就是以**父元素**作为参照点（父元素的定位不能是static），当前元素相对于父元素左边的偏移量。那么offsetTop就是以父元素为参照物，当前元素相对于父元素上边的偏移量。如果没有父元素那么参照点就是body。
>
> 这里要注意一点，如果当前定位元素本身是固定定位(position:fixed;)，那么就别费心找爹了，返回的是当前元素与可视窗口的距离。
>
> style.left/style.top和offsetLeft/offsetTop的功能一样，那么它们有什么区别呢？
>
> 1.返回值不一样：style.left/style.top返回的是字符串，带了单位（px）的，而offsetLeft/offsetTop只返回数字（小数会四舍五入）。
>
> 2.可读写性不同：offsetLeft/offsetTop只读，而style.left/style.top 可读写。
>
> ![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/4/1/162804163d195550~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
>
> * `offsetWidth和offsetHeight`
>
>
> 这两个也是**只读属性**  **offsetHeight || offsetWidth = boder + padding + content（不包括margin）**
>
> **offsetHeight/offsetWidth和style.height/style.width的区别**
>
> 1.返回值不一样：offsetHeight/offsetWidth返回纯数字（小数会四舍五入），style.height/style.width返回字符串，带单位（px）。
>
> 2.可读写性不一样：offsetHeight/offsetWidth只读，style.height/style.width可读写。
>
> 3.style.height/style.width是不包含边框的哦。还是用和公式表示一下：offsetWidth = style.width + style.padding + style.border
>
> * `clientWidth和clientHeight`
>
> **只读属性**，返回当前节点的**可视宽度**和**可视高度**（不包括边框、外边距）（包括内边距）clientHeight = topPadding + bottomPadding+ contentHeight
>
> * `scrollTop、scrollLeft、scrollWidth、scrollHeight`
>
> scrollTop和scrollLeft是**可读写属性** 。scrollTop：返回网页滚动条垂直方向滚去的距离； scrollLeft：返回网页滚动条水平方向滚去的距离；
>
> scrollWidth和scrolltHeight是**只读属性**，返回当前节点的实际宽度和实际高度（不包括边框）,没有滚动条时和clientWidth和clientHeight一样
>
> ![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/4/1/1628055d0479d7c5~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
>
> *  `event.clientX、event.clientY、event.pageX、event.pageY`
>
> event.clientX /event.clientY是目标点距离浏览器可视范围的X轴/Y轴坐标
>
> event.pageX /event.pageY 是目标点距离document最左上角的X轴/Y轴坐标

# 几种position

>position:`static` `relative` `absolute` `sticky`  `fixed` `unset`
>
>如果没有设置position为`relative` `fixed` `absolute` `sticky`，中的一种，那么`left` `top`属性时不起作用的
>
>`static`
>
>该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 `top`, `right`, `bottom`, `left` 和 `z-index `属性无效。
>
>`relative` 
>
>该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。position:relative 对 table-*-group, table-row, table-column, table-cell, table-caption 元素无效。
>
>`absolute`
>
>元素会被移出正常文档流，并不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。
>
>`fixed`
>
>元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。
>
>`realtive`结合`absolute`的经典例子，把父元素(demo2)设置成为`relative`，其内部子元素设置为`absolute`可以很方便的在父元素内部实现居中布局，角落布局，而且不会影响到其他元素
>
>```html
><style>
>    .demo2 {
>        width: 500px;
>        background-color: #8CC7B5;
>        height: 500px;
>        display: inline-block;
>        position: relative;
>        left: 1000px;
>    }
></style>
><div class="demo2">
>    <div style="height: 220px;width: 220px;background-color: #D1BA74;position: absolute;left: 50%;top: 50%;transform: translate(-50%,-50%)">
>        内容
>    </div>
>    <div style="height: 60px;width: 60px;background-color: #D1BA74;position: absolute;left: 0">
>        自制
>    </div>
>    <div style="height: 60px;width: 60px;background-color: #D1BA74;position: absolute;right: 0">
>        独家
>    </div>
>    <div style="height: 60px;width: 60px;background-color: #D1BA74;position: absolute;left: 0;bottom: 0">
>        1080P
>    </div>
>    <div style="height: 60px;width: 60px;background-color: #D1BA74;position: absolute;right: 0;bottom: 0">
>        最新
>    </div>
></div>
><div class="demo3">
></div>
>```
>
>![image-20220330151413135](E:\work\notebook\image-20220330151413135.png)

# 水平居中和垂直居中

>* flex布局
>
>```html
><div class="demo1" style="display: flex;justify-content: center;align-items: center">
>    <div style="width: 100px;height: 100px;background-color: #D1BA74">
>
>    </div>
></div>
>```
>
>* `absolute` + `relative` + `transform`
>
>```html
><div class="demo1" style="position: relative">
>    <div style="position: absolute;width: 100px;height: 100px;background-color: #D1BA74;left: 50%;top: 50%;transform: translate(-50%,-50%)">
>
>    </div>
></div>
>```
>
>* `margin` + `absolute` + `realtive`
>
>```html
><div class="demo1" style="position: relative">
>    <div style="width: 100px;height: 100px;background-color: #D1BA74;margin: auto;position: absolute;left: 0;right: 0;top: 0;bottom: 0">
>
>    </div>
></div>
>```

# 文本自动换行

>```html
>强制不换行
>white-space:nowrap;
>自动换行
>word-wrap:break-word;
>超出显示省略号
>text-overflow:ellipsis;
>overflow:hidden;
>多行文本超过x行显示省略号
>overflow: hidden;
>display: -webkit-box;
>-webkit-line-clamp: 3;
>-webkit-box-orient: vertical;
>```
>
>**以下的属性都只能用于p标签**
>
>* 单行文本超出显示省略号
>
>```css
>overflow:hidden;
>text-overflow:ellipsis;
>white-space:nowrap
>```
>
>* 多行文本超过X行显示省略号
>
>```css
>word-break: break-all;
>text-overflow: ellipsis;
>display: -webkit-box;
>-webkit-box-orient: vertical;
>-webkit-line-clamp: 2; /* 这里是超出几行省略 */
>```

# flex布局

>flex布局是一维布局，有两根交叉轴，主轴和交叉轴，flex容器和flex子项的属性在最后两张图
>
>## flex容器布局
>
>* flex-direction: row(水平方向，起点左端) | row-reverse(水平方向，起点右端) | column | column-reverse;
>
>flex-direction属性决定了主轴的方向，默认是水平方向
>
>*   flex-wrap: nowrap | wrap(自动换行) | wrap-reverse(自动换行，第一行在下面);
>
>flex-wrap控制换行，默认不可能换行，
>
>* justify-content: flex-start | flex-end | center | space-around | space-between | space-between;
>
>定义了主轴上的对齐方式
>
>![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bbc1f587b35248e8ac9e22c2f65e74e1~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)
>
>align-items: flex-start | flex-end | center | baseline（项目的第一行文字的基线对齐） | stretch（默认值）: 如果项目未设置高度或设为auto，将占满整个容器的高度。;
>
>定义项目在交叉轴上如何对齐
>
>![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8d13305de6a04c67b080c2c342949a13~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)
>
>* align-content: flex-start | flex-end | center | space-between | space-around | stretch;
>
>定义了多根轴线的对齐方式，前提是需要设置flex-wrap: wrap，否则不会有效
>
>![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7aef6b1eaf9242cc99ec31823c8606e6~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)
>
>## flex子项布局
>
>* `order` 属性定义项目的排列顺序。数值越小，排列越靠前，默认为0，可以是负数。

参考 https://juejin.cn/post/7019075844664459278#heading-9

flex布局的三个应用

等高 两栏自适应 三栏自适应 粘性页脚