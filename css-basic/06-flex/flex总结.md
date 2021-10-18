**开始使用**

开始使用flexbox,必须让父元素变成一个flex容器

flex容器: 父元素显示设置了display:flex

flex项目: flex容器内的子元素

有六个对齐属性可以使用在flex容器上

### flex-direction

控制flex项目沿着主轴的排列方向

flex-direction: row || column || row-reverse ||column-reverse

### flex-wrap

当希望flex容器内的flex项目达到一定数量时,能换行排列,把flex-wrap设置成wrap就有这个可能

flex-wrap : wrap || nowrap || wrap-reverse

### flex-flow

flex-flow是flex-direction和flex-wrap两个属性的速记属性

类似于border: 1px  solid red

例: 

```shell
ul {
	flex-direction: row
	flex-wrap: wrap
}
```

### justify-content(横向)

justify-content: flex-start || flex-end || center || space-between || space-around

- flex-start  靠左端对齐
- flex-end 靠右端对齐
- center 中间对齐
- space-between  两端对齐
- space-around  每个具有相同的空间

### align-items(纵向)

align-items: flex-start || flex-end || center || stretch || baseline

默认值是stretch 让所有的flex项目和flex容器高度一样

- flex-start  顶部对齐
- flex-end   底部对齐
- center  居中对齐
- baseline  基线对齐