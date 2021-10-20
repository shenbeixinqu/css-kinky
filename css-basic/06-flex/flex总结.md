## 容器属性

**开始使用**

开始使用flexbox,必须让父元素变成一个flex容器

```shell
.contrainer {
	display: flex || inline-flex
}
# 注意  当设置flex布局之后,子元素的float,clear,verticle-align的属性将会失效
```



flex容器: 父元素显示设置了display:flex

flex项目: flex容器内的子元素

有六个对齐属性可以使用在flex容器上

### flex-direction

```shell
控制flex项目沿着主轴的排列方向

flex-direction: row || column || row-reverse ||column-reverse
默认值: row 主轴为水平方向,起点在左端
	   row-reverse 主轴为水平方向,起点在右端
	   column 主轴为垂直方向,起点在上沿
	   column-reverse 主轴为垂直方向,起点在下沿
```

### flex-wrap

```shell
决定容器内项目是否可换行
flex-wrap : wrap || nowrap || wrap-reverse
默认值: nowrap  不换行,主轴尺寸空间不足时,项目尺寸会随之调整而并不会被挤到下一行
	   wrap 项目主轴尺寸超出容器时换行,第一行在上方
	   wrap-reverse 换行,第一行在下方
```

### flex-flow

```shell
flex-flow是flex-direction和flex-wrap两个属性的速记属性

类似于border: 1px  solid red
例:
ul {
	flex-direction: row
	flex-wrap: wrap
}
```

### justify-content(横向)

```shell
定义了项目在主轴的对齐方式
justify-content: flex-start || flex-end || center || space-between || space-around
```

- flex-start  靠左端对齐
- flex-end 靠右端对齐
- center 中间对齐
- space-between  两端对齐
- space-around  每个具有相同的空间

### align-items(纵向)

```shell
定义了项目在交叉轴的对齐方式
align-items: flex-start || flex-end || center || stretch || baseline

默认值: stretch, 项目未设置高度或者设置为auto,将占满整个容器的高度
	  - flex-start  顶部对齐
      - flex-end   底部对齐
      - center  居中对齐
      - baseline  基线对齐	
```

### align-content

```shell
定义了多根轴线的对齐方式,如果项目只有一根轴线,那么该属性将不起作用
align-content: flex-start || flex-end || center || space-between || space-around || stretch

当flex-wrap 设置为nowrap的时候,容器仅存在一根轴线,项目不会换行,就不会产生多条轴线
当flex-wrap 设置为wrap的时候,容器就会出现多条轴线,这时就需要设置多条轴线的对齐方式
```

## 项目属性

### order

```shell
定义项目在容器中的排列顺序,数值越小,排列越靠前,默认值为0
.item {
	order: <integer>
}
```

### flex-basic

```shell
定义了在分配多余的空间之前,项目占据的主轴空间,浏览器根据这个属性,计算主轴是否有多余空间,浏览器根据这个属性,计算主轴是否有多余空间
.item {
  flex-basic: <length> | auto
}
默认值: auto 即项目本来的大小,这时候item的宽高主要取决于width 和 height的值
当主轴为水平方向的时候,设置了flex-basic,项目的宽度设置值会失效,flex需要和flex-grow和flex-shrink配合使用才能发挥效果
当flex-basic 值为0%时,是把该项目视为零尺寸的,即使声明该尺寸为140px,也并没哟什么用
当flex-basic值为auto时,则根据尺寸的设定值(假如为100px),则这100px不会纳入剩余空间
```

### flex-grow

```shell
定义项目的放大比例
item {
	flex-grow
}
默认值是0,如果存在剩余空间,也不放大
当所有的项目都以flex-basic 进行排列后,仍有剩余空间,这时flex-grow发挥作用
如果所有项目的flex-grow属性都为1,则它们将等分剩余空间
如果一个项目的flex-grow属性为2,其他项目为1,则前者占据的剩余空间将比其他项多一倍
当其他项目以flex-basic的值排列完发现空间不够,此时flex-grow则不起作用了
```

### flex-shrink

```shell
.item {
	flex-shrink: <number>
}
默认值: 1,如果空间不足,该项目将缩小,负值对该属性无效
如果所有项目的 flex-shrink 属性都为 1，当空间不足时，都将等比例缩小。
如果一个项目的 flex-shrink 属性为 0，其他项目都为 1，则空间不足时，前者不缩小。
```

### flex:flex-grow,flex-shrink,flex-basic的简写

```shell
flex的默认值是三个属性值的组合
当flex取值为一个非负数字,则该数字为flex-grow值,flex-shrink取1,flex-basis取0%
如下是等同的:
.item {flex : 1}
.item {
	flex-grow: 1
	flex-shrink: 1
	flex-basis: 0%
}
当flex取值为0时,对应的三个值为 0 1 0%
.item {flex: 0}
.item {
	flex-grow: 0;
	flex-shrink: 1;
	flex-basis: 0%
}
当flex取值为一个长度或百分比,则视为flex-basis值,flex-grow取1,flex-shrink取1
.item {flex: 0%}
.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0%
}

.item {flex: 24px}
.item { 
	flex-grow: 1
	flex-shrink: 1
	flex-basis: 24px
}
当flex取值为一个非负数字和一个长度或百分比,则分别视为flex-grow和flex-basis的值,flex-shrink取1
.item {flex: 11 32px}
.item {
	flex-grow: 11
	flex-shrink: 1;
	flex-basis: 32px
}
```

### flex-wrap,flex-shrink,flex-grow之间关系

```shell
1.当 flex-wrap 为 wrap | wrap-reverse，且子项宽度和不及父容器宽度时，flex-grow 会起作用，子项会根据 flex-grow 设定的值放大（为0的项不放大）
2.当 flex-wrap 为 wrap | wrap-reverse，且子项宽度和超过父容器宽度时，首先一定会换行，换行后，每一行的右端都可能会有剩余空间（最后一行包含的子项可能比前几行少，所以剩余空间可能会更大），这时 flex-grow 会起作用，若当前行所有子项的 flex-grow 都为0，则剩余空间保留，若当前行存在一个子项的 flex-grow 不为0,则剩余空间会被 flex-grow 不为0的子项占据
3.当 flex-wrap 为 nowrap，且子项宽度和不及父容器宽度时，flex-grow 会起作用，子项会根据 flex-grow 设定的值放大（为0的项不放大）
4.当 flex-wrap 为 nowrap，且子项宽度和超过父容器宽度时，flex-shrink 会起作用，子项会根据 flex-shrink 设定的值进行缩小（为0的项不缩小）。但这里有一个较为特殊情况，就是当这一行所有子项 flex-shrink 都为0时，也就是说所有的子项都不能缩小，就会出现讨厌的横向滚动条
5.总结上面四点，可以看出不管在什么情况下，在同一时间，flex-shrink 和 flex-grow 只有一个能起作用，这其中的道理细想起来也很浅显：空间足够时，flex-grow 就有发挥的余地，而空间不足时，flex-shrink 就能起作用.当然，flex-wrap 的值为 wrap | wrap-reverse 时，表明可以换行，既然可以换行，一般情况下空间就总是足够的，flex-shrink 当然就不会起作用
```

### align-self

```shell
允许单个项目与其他项目不一样的对齐方式
单个项目覆盖align-items定义的属性
默认值是auto,表示继承父元素的align-items属性,如果没有父元素,等同于stretch
.item {
	align-self: auto || flex-start || flex-end || center || baseline || stretch
}
属性与align-items相同,align-self是对单个项目生效的,而align-items是对容器下的所有项目生效的
```

