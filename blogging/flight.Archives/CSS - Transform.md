## Title/ CSS Transform完全指南(第二版) #flight.Archives007
> 序: 第7天了! 终身学习, 坚持创作, 为生活埋下微小的信仰. 我是`忘我思考`,共同进步!
>
> 简介: 一篇最简约高效的CSS Transform教程.

### Tag/ Transform介绍
CSS的 `transform` 可以让元素产生变形效果,比如旋转,缩放,倾斜或平移
```css
element {
    transform: scale(0.5) translate(10px, 10px); /*`transform` 支持同时指定多个函数.*/
}
```
上面代码中 element 会缩放一半大小, 同时向右和向下各平移 10px.

接下来逐一介绍现支持的所有 Transform 函数.

### Tag/ Transform 函数介绍 
#### Matrix(矩阵计算)相关函数 
1. `matrix3d(a1, b1, c1, d1, a2, b2, c2, d2, a3, b3, c3, d3, a4, b4, c4, d4)`

   这个函数涉及高等数学知识, 矩阵变换, 使用非常复杂 ,随后介绍的`rotate`, `scale`, `skew`, `translate` 函数都是基于这个 `matrix` 函数实现的  
   
   但是在实战中直接使用这个函数的情况不大, 多数是间接使用基于该方法实现的函数, 所以本文不详细介绍该方法.

   就像Canvas中的 `webgl`, 在实战中一般都是使用基于 `webgl` 实现的JS库, 如 `three.js`
   
   关于 `matrix矩阵` 的详细内容可以参见 https://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-矩阵/

2. `matrix(a, b, c, d, tx, ty)`

   这个函数是 `matrix3d(a, b, 0, 0, c, d, 0, 0, 0, 0, 1, 0, tx, ty, 0, 1)` 的简写形式.

#### Perspective(透视深度)相关函数
3. `perspective(l)`
    
   `l`: `<length>`, 表示透视深度, 在值为正数时生效

#### Rotate(旋转)相关函数
4. `rotate3d(x, y, z, a)`

   `x`,`y`,`z`,`a`: `<angle>`, 横坐标, 纵坐标, Z坐标 和 顺时针旋转的角度

5. `rotate(a)`

   `a`: `<angle>`, 表示顺时针旋转的角度 

6. `rotateX(a)`

   `a`: `<angle>`, 表示横坐标旋转的角度

7. `rotateY(a)`

   `a`: `<angle>`, 表示纵坐标旋转的角度

8. `rotateZ(a)`

   `a`: `<angle>`, 表示Z坐标旋转的角度 

#### Scale(缩放)相关函数
9. `scale3d(sx, sy, sz)`

   `sx`, `sy`, `sz`: `<percentage>`, 在X轴, Y轴, Z轴上的缩放大小. 

   参数取值为 `1` 时不进行缩放处理, 在 `[0~1]` 区间按比例缩小, 在 `[>1]` 时按比例放大. 
   
   参数取负值时元素将沿原点中心翻转.

10. `scale(sx, [sy])`

    `sx`, `sy`(可选): `<percentage>`, 在X轴, Y轴上的缩放大小.

11. `scaleX(s)`

    `s`: `<percentage>`, 在X轴上的缩放大小.

12. `scaleY(s)`

    `s`: `<percentage>`, 在Y轴上的缩放大小.

13. `scaleZ(s)`

    `s`: `<percentage>`, 在Z轴上的缩放大小.

#### Skew(倾斜)相关函数
14. `skew(ax, [ay])`

    `ax`, `ay`(可选): `<angle>`, 元素沿X轴和Y轴倾斜的角度

15. `skewX(a)`

    `a`: `<angle>`, 元素沿X轴倾斜的角度

16. `skewY(a)`

    `a`: `<angle>`, 元素沿Y轴倾斜的角度

#### Translate(平移)相关函数
备注: `translate` 是一个CSS属性, 可以单独使用, 用法与函数一致.

17. `translate3d(tx, ty, tz)`

    `tx`, `ty`, `tz`: `<length>`, 元素沿X轴,Y轴和Z轴平移的距离.
    
18. `translate(tx, [ty])`

    `tx`, `ty`(可选): `<length>`, 元素沿X轴和Y轴平移的距离.

19. `translateX(t)`

    `t`: `<length>`, 元素沿X轴平移的距离.

20. `translateY(t)`

    `t`: `<length>`, 元素沿Y轴平移的距离.

21. `translateZ(t)`

    `t`: `<length>`, 元素沿Z轴平移的距离.

### Tag/ Transform 相关属性介绍
1. `transform-origin`
   
   指定元素变形的原点, 默认值为 `center`.
   
   可取值:
   ```
   transform-origin: 2px; /*如果只有一个值, 则表示原点的横坐标*/
   
   transform-origin: 2px 2em; /*如果有两个值, 则分别表示原点的横坐标和纵坐标*/
   
   transform-origin: left top; /*可以使用关键字: left, center, right, top 或 bottom*/
   
   transform-origin: top right; /*如果两个值都是关键字, 则可以先纵坐标, 后横坐标*/
   
   transform-origin: 20px left; /*这是错误的表示. 如果关键字和长度单位同时使用, 不可以都表示纵坐标或横坐标*/
   
   transform-origin: 2px 10% 20px; /*如果有三个值, 则前两个值用法不变, 第三个值表示原点的深度(Z坐标)*/
   ```

2. `transform-style`

   指定元素的子元素是位于 3D 空间中还是平面中, 默认值是 `flat`.

   可取值:
   ```
   transform-style: flat; /*子元素位于独立的平面*/
   
   transform-style: preserve-3d; /*子元素位置继承自父元素的3d位置*/
   ``` 

3. `transform-box`

   指定变形的布局框

   可取值
   ```
   /*不了解CSS Box Model的, 可以去搜一下, 本文不详细介绍.*/
   transform-box: content-box /*使用内容框为盒布局方式*/
   
   transform-box: border-box /*使用边框框为盒布局方式*/
   
   transform-box: fill-box /*使用填充边界框为盒布局方式, 填充边界框是仅包含元素几何形状的框. 对于基本形状, 这是填充的区域.*/
   
   transform-box: stroke-box /*使用描边框为盒布局方式. 描边框是包含元素的几何形状及其笔画形状的边界框.*/
   
   transform-box: view-box /*使用最近父元素的SVG Viewport为盒布局方式*/
   ``` 

4. `perspective`

   可以独立为一个CSS属性, 指定透视深度, 和作为函数使用方法一致.

5. `perspective-origin`

   指定了3d观察者的位置, 值为 `perspective` 属性的消失点

   可取值:
   ```
   /*x-position 和 y-position 都是 <length-percentage> 值, 可取负值*/
   
   /*
   可使用的关键字: 
   x-position: left(0%), center(50%), right(100%)
   y-position: top(0%), center(50%), bottom(100%)
   */
   
   perspective-origin: x-position; /*一个值*/

   perspective-origin: x-position y-position; /*两个值*/

   perspective-origin: y-position x-position; /*如果两个值都是关键字, 先y后x也是允许的*/
   ``` 

<!--
### ->> Details

### ->> flight.frontendBeautiful
> 待添加

### ->> flight.Player
> 待添加

### ->> flight.Playground
> 待添加

### ->> flight.QuickDemo
> 待添加

### ->> See also
> 待添加
-->

### ->> Reference link
> MDN中文文档 https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform
>
> MDN 英文文档 https://developer.mozilla.org/en-US/docs/Web/CSS/transform
> 
> `transform-origin`属性介绍 https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-origin
>
> CSS-Tricks https://css-tricks.com/almanac/properties/t/transform/
> 
> Quackit https://www.quackit.com/css/css3/properties/css_transform-box.cfm
> 
> 张鑫旭 - Matrix矩阵 https://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-矩阵/ 
> 
> 张鑫旭 - CSS动画 https://www.zhangxinxu.com/wordpress/2010/11/css3-transitions-transforms-animation-introduction/

### ->> Version History
> 现在版本为V2.1, 下一版预计添加几处 flight.Playground(hover QuickView) 以便互动式理解
> 
> 详见 Github(@flightmakers)
>
> 2021.8.17 在掘金发布V0.1
> 
> 2021.8.18 补全内容. 发布V1.0, 添加了两个链接
> 
> 2021.8.24上午 补全了许多其他Transform属性,发布V2
> 
> 2021.8.24中午 又添加了两个透视属性, 发布V2.1