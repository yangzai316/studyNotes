## Flex 布局
2009年，W3C提出新的布局方案，Flexible Box 的缩写，意为"弹性布局"。<br>
任何一个容器都可以指定为 Flex 布局。<br>
注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。
#### 一 前言
采用flex布局的元素，成为‘flex容器’，元素的子元素则自动成为元素的容器成员，成为‘flex项目’。<br>
容器默认存在两根轴：<br>
水平的**主轴（main axis）**和垂直的**交叉轴（cross axis）**；<br>
主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；<br>
交叉轴的开始位置叫做cross start，结束位置叫做cross end；<br> 
项目默认沿主轴排列；<br>
单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。
#### 二 容器的属性
flex-direction<br>
flex-wrap<br>
flex-flow<br>
justify-content<br>
align-items<br>
align-content<br>

- flex-direction
决定主轴的方向，即项目排列的方向

属性值|描述
--|:--:
row |水平方向，起点在左端
row-reverse |水平方向，起点在右端
column |垂直方向，起点在上沿
column-reverse|垂直方向，起点在下沿

- flex-wrap
默认情况，项目排于一行，flex-warp决定项目如何换行

属性值|描述
--|:--:
nowrap |（默认）不换行
wrap |换行，第一行在上面
wrap-reverse|换行，第一行在下面

- flex-flow
是【flex-direction】【flex-warp】的组合，默认值为：“row nowarp”

- justify-content
决定项目在主轴上的对齐方式

属性值|描述
--|:--:
flex-start |（默认）向左对齐
flex-end |向右对齐
center| 居中 
space-between|两端对齐，项目中间间隔相同
space-around|两端存在间隙，项目中间间隔相同，类似设置“margin:0 10px",故左右距离是项目之间间距的一半

- align-items
决定项目在交叉轴上的对齐方式

属性值|描述
--|:--:
flex-start |交叉轴的起点对齐
flex-end|交叉轴的终点对齐
center|交叉轴的中心对齐
baseline|交叉轴的第一行字的基线对齐
stretch|(默认值)项目被拉伸，以适应容器，当对应轴已设置width/height时，以width/height值为主

- align-content
定义多个轴线时，轴线的对齐方式，单个轴线时，该属性无效

属性值|描述
--|:--:
flex-start |交叉轴的起点对齐
flex-end|交叉轴的终点对齐
center|交叉轴的中心对齐
space-between|两端对齐，项目中间间隔相同
space-around|两端存在间隙，项目中间间隔相同，类似设置“margin:0 10px",故左右距离是项目之间间距的一半
stretch|（默认）每轴线占满整个交叉轴

#### 三 项目的属性
order<br>
flex-grow<br>
flex-shink<br>
flex-basis<br>
flex<br>
align-self<br>

- order
定义项目排列的顺序，值越小（可为负值），则越靠前，默认 0 。

- flex-grow 
定义项目放大的比例，默认为 0 （表示存在多余的空间，不放大）

- flex-shrink
定义项目缩小的比例，默认为1（表示空间不足时，该项目将缩小）<br>
当所有项目该值都为1，则空间不够会等比缩小；存在值为 0 ，则该项目将不会缩小。

- flex-basis
在分配多余空间之前，项目占据的主轴空间。浏览器会根据这个属性值来计算是否还有多余空间。默认为 auto， 即项目原本大小，可以设置为width/height的值（100px)作为项目占据的固定空间。

- flex
flex是flex-grow、flex-shrink、flex-basis的简写，默认为“0 1 auto"，后两个属性可选。

- align-self
项目设置该属性，则允许该项目违背父级的align-items属性，设置自己的交叉轴的对齐方式

属性|描述
--|:--:
auto|默认值为auto，表示继承父级的align-items属性，如果没有父级，则为 stretch
flex-start|交叉轴的起点对齐
flex-end|交叉轴的终点对齐
center|交叉轴的中心对齐
baseline|每个项目的第一行文字底线对齐
stretch|拉伸项目

参考文章：*[  基础前端项目部署-简记](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)*
