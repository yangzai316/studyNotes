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
* 选择所有元素
#### 子代选择器
[element/.class/#id/...]>[element/.class/#id/...] 选择父级下直接子代元素（如果元素不是父元素的直接子元素(孙子级别的不行），则不会被选择）。
#### 相邻兄弟元素选择器 
[element/.class/#id/...]+[element/.class/#id/...] 选择指定的元素之后紧跟的元素。
#### 属性选择器
element[target] 选择所有带有target属性的element元素。<br>
element[target=yang] 选择所有使用target="yang"的element元素。<br>
element[target~=yang] 选择属性包含单词"yang"的所有element元素(是单词，不是对应字母)。<br>
element[target|=yang] 选择target属性的起始值="yang"的所有元素(值是整个单词，单独像target="yang"，或者使用连字符(-)，如target ="yang-xxx")。
#### 伪类选择器
:focus 选择具有焦点的元素。<br>
element:first-child 选择element其父级的第一个子元素，且这个子元素需为element。<br>
:before 选择对象前插入内容（后期css3为了区分伪类和伪元素，用::before代替:before，但后者仍然可使用）。<br>
:after 选择对象后插入内容插入内容（同上）。<br>
element:lang(yang) 选择带有指定 yang 的 lang 属性的元素（值是整个单词，单独像lang="yang"，或者使用连字符(-)如lang ="yang-xxx"）。

