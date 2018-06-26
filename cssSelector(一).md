# css 选择器
CSS选择器用于选择你想要的元素的样式的模式，以下总结一下css各个版本的选择器，基础知识，大牛请绕道！
## css1选择器
css1选择器相对比较常用，不会过多介绍<br>
#### 类选择器
.class 选择带有指定类 (class) 的元素。
#### id选择器
#id 选择具有ID的元素的样式。
#### 元素选择器
element 选择指定元素名称的所有元素。
#### 后代选择器
[element/.class/#id/...] [element/.class/#id/...] 选择元素内部指定的元素(和子代选择器不同)。
#### 群组选择器
[element/.class/#id/...],[element/.class/#id/...] 选择需要具有相同的样式的元素，用逗号分隔每个元素的名称。
#### 伪类选择器
:xxx 伪类用于向某些选择器添加特殊的效果。
链接的不同状态都可以不同的方式显示，这些状态包括：
``` css
a:link {color: #FF0000}		  /* 未访问的链接 */
a:visited {color: #00FF00}	/* 已访问的链接,自行测试这个功能，最好使用真实链接，空和#都会出现问题 */
a:hover {color: #FF00FF}	  /* 鼠标移动到链接上 */
a:active {color: #0000FF} 	/* 选定的链接,即点击那一刹那的变化*/
```
css1还有其他的伪类选择器<br>
:first-letter 选择元素的首字母。<br>
:first-line 选择元素的首行。

## css2选择器
#### 通配符选择器
\* 选择所有元素
#### 子代选择器
[element/.class/#id/...]>[element/.class/#id/...] 选择父级下直接子代元素（如果元素不是父元素的直接子元素(孙子级别的不行），则不会被选择）。
#### 相邻兄弟元素选择器 
[element/.class/#id/...]+[element/.class/#id/...] 选择指定的元素之后紧跟的元素。
#### 属性选择器+
element[target] 选择所有带有target属性的element元素。<br>
element[target=yang] 选择所有使用target="yang"的element元素。<br>
element[target~=yang] 选择属性包含单词"yang"的所有element元素(是单词，不是对应字母)。<br>
element[target|=yang] 选择target属性的起始值="yang"的所有元素(值是整个单词，单独像target="yang"，或者使用连字符(-)，如target ="yang-xxx")。
#### 伪类选择器+
:focus 选择具有焦点的元素。<br>
element:first-child 选择element其父级的第一个子元素，且这个子元素需为element。<br>
:before 选择对象前插入内容（后期css3为了区分伪类和伪元素，用::before代替:before，但后者仍然可使用）。<br>
:after 选择对象后插入内容插入内容（同上）。<br>
element:lang(yang) 选择带有指定 yang 的 lang 属性的元素（值是整个单词，单独像lang="yang"，或者使用连字符(-)如lang ="yang-xxx"）。


## css3选择器
重点是css3选择器，随着浏览器的不断升级和IE的落寞和妥协，现在使用css3的兼容性问题越来越小，必须赶紧Get。
#### 相邻兄弟选择器+
element1~element2 选择在 element1 后面的所有element2；element1 和 element2 这两种元素必须具有相同的父元素，但 element2 不必紧跟在 element1 的后面。
#### 属性选择器++
element[target^="yang"] 选择属性值带指定的值yang开始的所有元素element(是element[target|=yang]加强版)。<br>
element[target$="yang"] 选择属性值带指定的值yang结尾的所有元素element。<br>
element[target*="yang"] 选择属性值含有指定值yang的所有元素element。
#### 伪类选择器++
element:first-of-type 选择其父级的第一个子element元素(该element可以不是其父级的第一个元素，和:nth-of-type(1)同效果)。<br>
element:last-of-type 选择其父级的最后一个子element元素（同上，和:nth-last-of-type(1)同效果，注意和:last-child的区别）。<br>
element:only-of-type 选择其父级下只有唯一一个element元素（如：其父级有很多子元素，只有一个p元素，就可以用这个方法选择,注意和only-child的区别)。<br>
element:only-child 选择其父元素中只含有一子元素且为element的元素。<br>
element:nth-child(n) 选择其父元素中的第n个子元素。<br>
element:nth-last-child(n) 选择其父元素中的倒数第n个子元素。<br>
element:nth-of-type(n) 选择其父元素中同类型（都是element）中的第n个同级兄弟元素。<br>
element:nth-last-of-type(n) 选择其父元素中同类型（都是element）中的倒数第n个同级兄弟元素。<br>
element:last-child 选择器其父元素中最后一个子元素(最后一个元素必须为element,注意和:last-of-type的区别)。<br>
:root 选择文档的根元素,在HTML中根元素始终是HTML元素。
:empty 选择没有任何子级的元素（包括文本节点）。
:target 和锚点配合使用 # 锚的名称是在一个文件中链接到某个元素的URL，元素被链接到目标元素；:target可选择跳转到target元素。
:enabled 选择每个启用的的表单元素（主要用于表单元素，与:disabled相反）。
:disabled 选择每个禁用的的表单元素（主要用于表单元素，与:enabled相反）。
:checked 选择每个选中的输入表单元素（仅适用于单选按钮或复选框）。
:not(element) 选择每个不是指定的元素的剩余元素。
::selection 选择元素中被用户选中或处于高亮状态的部分(选中某段文案),只可以应用于少数的CSS属性：color, background, cursor,和outline。
:out-of-range 选择元素的值在指定区间之外时，只作用于能指定区间之外值的元素，例如 input 元素中的 min 和 max 属性。












