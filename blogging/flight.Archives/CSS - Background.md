## Title/ CSS Background&Gradient完全指南 #Archives009
> 序:  
> 关于 `background` 属性, 了解点CSS的人总会知道个大概.  
> 但是你肯定多半还有点不会的吧(别在这装!), 比如你能手写CSS的6个渐变函数吗? 你知道bg-repeat中space和round的作用吗? 你能用纯CSS实现AI中的"任意渐变"吗?  
> 这篇文章详细的整理了一遍CSS的Background和Gradient属性的各种诡异用法.  
> 当然照顾萌新, 讲的会比较完整和基础, 进阶开发者可以只关心你需要的内容, 不必顺序阅读.
> 
> 简介:  
> 一篇最全CSS背景, 渐变教程!
> 
> 注:  
> `background` 属性在本文中会图个方便缩写为bg, 不过在CSS中不能这样简写.

### Tag/ Background介绍
CSS 属性 `background` 可以为网页上的元素制作出来各种丰富多彩的背景.  
不仅可以搞6种渐变色, 还可以在一个元素叠加多个背景, 在实现一些复杂效果的时候还是蛮有用的.

来段代码:
```css
element {
    background:
        url(mi_logo.svg)    /* image */
        top center / 20px 20px /* position / size */
        no-repeat /* repeat */
        fixed /* attachment */
        padding-box /* origin */
        content-box /* clip */
        orange /* color */
} 
```
上面就是 `background` 属性的大致使用方法了.  `background` 属性也可以进行叠加:
```css
ele {
   background: cornflowerblue, url("ruok.svg");
}
```
属性之间用空格分开, 不同背景层之间用逗号分开.

### Tag/ Background相关属性
1. `background`
   
   这个属性是`background-clip`, `background-color`, `background-image`, `background-origin`, `background-position`, `background-repeat`, `background-size` 和 `background-attachment` 属性的 `CSS简写属性`, 接下来介绍每个属性的用法.
   
   可取值:
   ```
   background: bg-color bg-image bg-position/bg-size bg-repeat bg-origin bg-clip bg-attachment, (another-bg);
   /* 部分属性之间可以交换位置, 要注意 bg-position/bg-size 中间的 / 不能省略. */
   ``` 

2. `background-color`

   指定了背景颜色, 值为 `<color>`, 默认值是 `transparent`.

3. `background-image`

   指定了一张背景图片, 可以是 `url(...)`(图片的资源地址, 作为背景图片插入网页), 可以是 `<color>`(可以理解为一张纯色图片), 也可以使用 `CSS渐变函数`(一张渐变色的图片).

   而CSS渐变使用是真的很复杂, 为了方便阅读这里只作引用, 使用方法和函数会在本文的 `->> Details` 中完整的展开介绍.
   
4. `background-position`

   指定背景图片的位置, 默认值为 `center`, 这个位置是相对于 `background-origin` 而言的.

   可取值:
   ```
   /*单位可以是 <length>, <percentage> 或者关键字, 可取负值表示相反方向偏移*/
   /*关键字: top, bottom, left, right, center. */
   
   background-position: 50px; /*一个值: 指定x坐标的值, 另一个值为center(默认值)*/
   background-position: top; /*一个值(关键字): 指定该关键字表示的值, 另一个值为center.*/
   background-position: 100px 75%; /*两个值: 分别是x坐标和y坐标的值*/
   background-position: bottom 25% right; /*三个值(关键字 值 关键字): 指定距离边际的距离(比如本例是距离底部25%长, 与右边贴合.)*/
   background-position: top right 50px; /*三个值(关键字 关键字 值): 指定距离边际的距离(本例是距离右边50px, 贴合顶部.)*/
   background-position: bottom 25% left 50px; /*四个值(关键字 值 关键字 值): 指定距离边际的距离(本例是距离底部25%长, 距离左边50px).*/
   ```

5. `background-size`
   
   指定背景图片的大小, 默认值为 `auto`.

   可取值:
   ```
   /*单位可以是 <length>, <percentage> 或者关键字*/
   /*关键字: contain(按比例缩放, 以较短边为图片大小填满背景区域), cover(按比例缩放, 以较长边为图片大小填满背景区域), auto(按比例缩放, 默认为原始大小)*/
   
   background-size: 50px; /* 一个值: 指定图片的宽度, 图片的高度为auto(默认值), 即按比例缩放大小*/
   background-size: auto 5em; /* 两个值: 分别指定图片的宽高*/
   ```

6. `background-repeat`

   指定背景图片的重复排列方法, 默认值为`repeat`.

   ```
   /*一个值: 同时指定x轴和y轴的重复排列方法.*/
   background-repeat: repeat; /*按需重复背景图片来覆盖整个背景区域. 在大小不够的情况下, 边缘的图片会被裁剪.*/
   background-repeat: space; /*重复背景图片来覆盖整个背景区域, 但是不会裁剪图片. 边缘图像会被固定边上, 同时空白会均匀地分布在图像之间. background-position属性会被忽视, 除非只有一个图像能被无裁剪地显示. 只在一种情况下裁剪会发生, 那就是图像太大了以至于没有足够的空间来完整显示一个图像.*/
   background-repeat: round; /*重复背景图片并按比例缩放以填充空间, 不会有空隙.*/
   background-repeat: no-repeat; /*不重复背景图像.*/
   
   /*两个值: 分别指定x轴和y轴的重复排列方法.*/
   background-repeat: space round; /*分别指定X轴和Y轴的重复方式为 space 和 round.*/
   
   /*简写方法*/
   background-repeat: repeat-x; /*作用与 repeat no-repeat 相同*/
   background-repeat: repeat-y; /*作用与 no-repeat repeat 相同*/
   ```

7. `background-origin`

   指定背景图片的起始点位置, 默认值为 `padding-box`.  
   特殊地, 当 `background-attachment` 属性值为 `fixed` 时, 该属性将被忽略不起作用.

   可取值:
   ```
   background-origin: border-box; /*背景图片左上角坐标位于 border-box 位置*/
   background-origin: padding-box; /*背景图片左上角坐标位于 padding-box 位置*/
   background-origin: content-box; /*背景图片左上角坐标位于 content-box 位置*/
   ```
   
   > See Also:  
   > 一个LiveDemo https://tympanus.net/codrops/css_reference/background-origin/
   > 
   > bg-origin和bg-clip区别(截图) https://www.cnblogs.com/shytong/p/5077129.html

8. `background-clip`
   
   指定背景(图片和颜色)延伸到哪个盒子, 默认值为 `border-box`.
   
   可取值:
   ```
   background-clip: border-box; /*背景延伸到 border-box*/
   background-clip: padding-box; /*背景延伸到 padding-box*/
   background-clip: content-box; /*背景延伸到 content-box*/
   background-clip: text; /*(Experimental) 背景填充文本*/
   ```

9. `background-attachment`

   指定背景图像的位置在元素内的滚动方式(固定还是随着元素滚动), 默认值为 `scroll`.

   可取值:
   ```
   background-attachment: fixed; /*表示背景相对于视口固定. 即使一个元素拥有滚动机制, 背景也不会随着元素的内容滚动.*/
   background-attachment: local; /*表示背景相对于元素的内容固定. 如果一个元素拥有滚动机制, 背景将会随着元素的内容滚动, 并且背景的绘制区域和定位区域是相对于可滚动的区域而不是包含他们的边框.*/
   background-attachment: scroll; /*表示背景相对于元素本身固定, 而不是随着它的内容滚动(对元素边框是有效的)*/
   ```

### ->> Details
#### `background-image` - `CSS渐变`函数
> 序:  
> 按说 CSS Gradient 这个专题可以独自成文了, 所以独立的写一个序.
> 
> 关于CSS渐变虽然大家都或多或少了解一些, 但是其实这个内容非常复杂, 大多数人都只是停留在表面(比如只会写最基本的两种渐变方法).
> 
> 但是你比别的普通前端厉害的地方就体现于你是否知道别人不懂的东西! 而这个CSS渐变在UI设计中也是很常用的, UI设计师很可能为了折磨前端, 做一些神奇又复杂的渐变.  
> 
> 比如你在实战中要还原设计稿, Adobe Illustrator里的渐变也可一点也不简单(图片来自Adobe官网).  
> 
> ![](https://img2020.cnblogs.com/blog/2451762/202108/2451762-20210825115709569-1347013995.png)
> 
> 比如上图中, Adobe就采用了"任意渐变"的Gradient Type.
> 
> 这个任意渐变的设计稿, 要你来实现, 大概会说: 这个渐变都不是在一条线的(到处都有黑色和白色的色标), 用一般的渐变根本没法实现啊...
> 
> 所以解决方法可能是用AI导出含渐变色的png(AI默认导出svg时就是这样实现的), 然后用bg-image(或者bg-clip: text)来添加到前端.
> 
> 倒不是这种方法不好, 只要能实现效果, 任何方法都是OK的.
> 
> 只是我觉得知难而退, 不肯钻研的的学习态度不是很好. 所以现在把它弄明白吧!
> 
> 看到这里你肯定已经猜到了, 纯CSS是可以实现"任意渐变"的!!! ->> 看下面!
> 
> ```
> background: radial-gradient(ellipse at right, #f18a89, transparent),
>             radial-gradient(ellipse at bottom, #e16259, transparent), 
>             radial-gradient(ellipse at left, #abdcef, transparent), 
>             linear-gradient(#fffefc, transparent);
> ```
> 
> 好, 那它会有什么效果呢?
> 
> ![](https://img2020.cnblogs.com/blog/2451762/202108/2451762-20210825122537483-1896391413.png)
> 
> 是不是有内味了? 只要把颜色换成黑色和白色, 调整一些参数, Illustrator中的"任意渐变"好像也不是那么复杂!
> 
> 可是现在网上的关于CSS渐变的**`完整`**资料非常少, 连MDN目前都有中文支持性问题(见下图, 翻译了一半就全是英文了), 所以我读英文官方文档看了半天才搞懂啊qwq...  
> 
> ![](https://img2020.cnblogs.com/blog/2451762/202108/2451762-20210825020456784-650932240.png)
> 
> 而且菜鸟教程(runoob.com) 和W3School文档, 目前都只说有两个函数(最常用的线性渐变和径向渐变), 只介绍了最基础的使用方法, 而这在实战很多情况是不够的.  
> 
> 所以我决定把我的理解以最通俗易懂的方式放在这里, 分享给大家一篇(目前可能也是唯一一篇)最完整的中文文档.  
> 
> 准备好了没? 重头戏开始了!

CSS `<gradient>` 是 `<image>` 类型的一种, 所以不只是 `background` 可以用到它, `border-image` 等只要是图片都能用.

目前支持6种CSS渐变函数, 有3种是基本函数, 另外的3种都是重复渐变(凑数的)

1. `linear-gradient()`(线性渐变)
   
   语法:
   ```
   background: linear-gradient(angle, stop1, stop2, ...); 
   /*angle可选, 默认值为 to bottom. stop为色标*/
   
   linear-gradient(#e66465, #9198e5); 
   /*从上到下过渡荔枝红到鼠尾草蓝*/
   
   linear-gradient(90deg, green, yellow); 
   /*angle设为90度, 表示从左到右*/
   
   linear-gradient(to left, orange, yellow); 
   /*
   to <direction> 关键字, 表示渐变方向, 可取值有: 
   to top = 0deg, to bottom = 180deg, to left = 270deg, to right = 90deg
   */
   
   linear-gradient(to right bottom, black, white) 
   /*可以同时定义两个 <direction>, 表示向某个角渐变.*/
   
   linear-gradient(0.25turn, #3f87a6, #ebf8e1, #f69d3c); 
   /*0.25turn关键字, 表示从左到右. turn前的数字可以是 <percentage>, 表示旋转的大小.*/
   
   linear-gradient(#3f87a6, #ebf8e1 10% 50%, #f69d3c 30%); 
   /*
   对于每一个色标(<linear-color-stop>), 颜色后的 <percentage> 表示色标的所处区域, 如果有一个百分比表示色标的位置, 如果有两个表示一个区间. 
   如果不设置位置, 则为最相邻两个位置的平均值. 如果色标之间有重叠, 定义在之前的会覆盖之后的.
   */
   
   linear-gradient(pink, 25%, orange); 
   /*
   可以在两个色标之间加入 <percentage> 表示二者的过渡比例(<color-hint>), 如这个例子中粉色少, 橙色多. 
   具体的计算方法为: 在粉色和橙色两端中间隐式添加一个色标位于25%的点, 颜色是二者的平均值, 然后让二者都向这个添加的色标过渡.
   */
   ```
   
2. `radial-gradient`(径向渐变)

   语法:
   ```
   background: radial-gradient(position, stop1, stop2, ...) 
   /*position可选, 默认值为 center.*/
   
   radial-gradient(lime, yellow); 
   /*从内到外过渡青色到黄色*/
   
   radial-gradient(circle, lime, yellow);
   /*
   可以指定渐变形状(<ending-shape>), 默认值为 ellipse, 即会根据元素的长宽比对椭圆进行拉伸. 
   这里定义了 circle, 无论元素多大, 渐变色都是一个正圆. 
   具体的计算方法为: ellipse是根据长宽进行拉伸, circle是根据对角线的一半长度进行渐变.
   */
   
   radial-gradient(circle at 50px 25%, lime, yellow); 
   /*可以用 at 关键字指定位置(<position>), 表示渐变的起始点位置*/ 
   
   radial-gradient(50px circle, lime, yellow); 
   radial-gradient(30px 20px ellipse, lime, yellow); 
   /*可以在形状前添加 <length> 指定在圆的半径, 如果是椭圆可以有两个分别是横向和纵向.*/ 
   
   radial-gradient(closest-side circle at 50px 25%, lime, yellow); 
   /*
   有4个关键字可以指定渐变的终止点(也就是渐变区域的大小, <size>), 默认值为 farthest-corner, 添加在第一个参数中:
   closest-side : 渐变中心距离容器最近的边作为终止位置
   closest-corner : 渐变中心距离容器最近的角作为终止位置
   farthest-side : 渐变中心距离容器最远的边作为终止位置
   farthest-corner : 渐变中心距离容器最远的角作为终止位置
   */ 
   
   radial-gradient(circle, green 20%, lime, yellow 10% 50%); 
   /*
   可以在色标(<linear-color-stop>)后面添加一个或者两个 <percentage> 表示渐变区间.
   用法和作用与 linear-gradient() 中相同.
   */ 
   
   radial-gradient(closest-side circle at 50px 25%, lime, 20%, yellow); 
   /*
   可以在两个色标之间加入 <percentage> 表示二者的过渡比例(<color-hint>).
   用法和作用与 linear-gradient() 中相同.
   */ 
   ```

3. `conic-gradient`(圆锥渐变)
   
   语法:
   ```
   background: conic-gradient( from <angle> at <position>, <angular-color-stop-list>);
   /*from <angle> 和 at <position>可选. <angle> 默认值为 0deg, <postion> 默认值为 center*/
   
   conic-gradient(from 45deg, black, white); 
   /*from <angle> 指定起始角度*/
   
   conic-gradient(from 45deg at 25% 50px, black, white); 
   /*at <position> 指定中心点位置*/
   
   conic-gradient(from 45deg at 25% 50px, black, 75%, white); 
   /*同样可以指定过渡比例(<color-hint>)*/
   ```

4. , 5. , 6. `repeating-linear-gradient`, `repeating-radial-gradient`, `repeating-conic-gradient()`(重复渐变)
   ```
   background: 
    repeating-radial-gradient(
      circle at 0 0, 
      #eee,
      #ccc 50px
    );
   ```
   上面代码会显示这样的图像:

   ![](https://img2020.cnblogs.com/blog/2451762/202108/2451762-20210826180850467-717089065.png)

   重复渐变的语法与所对应的基本渐变完全一致, 但会根据原图像进行重复填充. 

哈~ OK了, 如果下次遇到关于Background&Gradient有不会的, 可以直接在这篇文章按 `ctrl(mac: command)+f` 速查. 或者有需要可以收藏.

<!--
### ->> flight.frontendBeautiful
> 待添加

### ->> flight.Player
> 待添加

### ->> flight.Playground
> 待添加
-->

### ->> See also
> Gradienta - 体验在线编辑CSS背景渐变 https://gradienta.io/
> 
> Codepen - Explaining gradient angles https://codepen.io/thebabydino/full/qgoBL
> 
> MDN - 渐变:  
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/linear-gradient()
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/radial-gradient()
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/conic-gradient()
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/repeating-linear-gradient()
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/repeating-radial-gradient()
> https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/repeating-conic-gradient()

### ->> Reference link
> MDN中文文档 https://developer.mozilla.org/zh-CN/docs/Web/CSS/background
>
> MDN 英文文档 https://developer.mozilla.org/en-US/docs/Web/CSS/background
> 
> 张鑫旭 https://www.zhangxinxu.com/wordpress/2017/11/css3-radial-gradient-syntax-example/
> 
> CSS-Tricks https://css-tricks.com/snippets/css/css-repeating-gradients/
>
> 菜鸟教程 https://www.runoob.com/cssref/css3-pr-background.html
>
> Sara Cope https://css-tricks.com/almanac/properties/b/background/
> 
> 掘金 - CSS Background 属性详解 https://juejin.cn/post/6844903463273381901
>
> MDN - 使用CSS渐变 https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Images/Using_CSS_gradients

### ->> Version History
> 现在版本为V1.0
> 详见 Github(@flightmakers)
>
> 2021.8.25(本来计划是2021.8.19的, 但是最后失败了) 发布V0.1
> 
> 2021.8.26 补全渐变相关内容, 发布V1.0
> 
> 终于写完啦(学废了)! 感觉有收获, 小明反手就给了个赞! 对我的另外一些作品感兴趣(比如JS this完全指南, 正则完全指南, Matrix()完全指南)可以进我主页继续学习! (cnblogs, Bilibili, Github都是一个名, 叫`忘我思考(@flightmakers)`
