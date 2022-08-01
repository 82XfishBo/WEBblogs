# jQuery基本功能

### 徐上博

**jQuery是目前使用最广泛同时也是最长寿的js函数库。**

*jQuery是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库（框架）于2006年1月由John Resig发布。jQuery设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。*

*jQuery的核心特性可以总结为：具有独特的链式语法和短小清晰的多功能接口；具有高效灵活的CSS选择器，并且可对CSS选择器进行扩展；拥有便捷的插件扩展机制和丰富的插件。jQuery兼容各种主流浏览器，如IE 6.0+、FF 1.5+、Safari 2.0+、Opera 9.0+等。*

对于网页开发者来说，学会jQuery是必要的。因为它让你了解业界最通用的技术，为将来学习更高级的库打下基础，并且确实可以很轻松地做出许多复杂的效果。

***

## 一、jQuery获取元素

jQuery基本的设计思想和主要用法便是**先选择好元素，再对其进行各种操作。**
所以使用jQuery的第一步便是先要获取到想要操作的元素。而在jQuery中便是将一个选择表达式放入构造函数jQuery()（jQuery里一般简写为$）中，然后得到选中的元素。

**选择表达式可以有以下两类：**

```js
1.css选择器；

   $(document) //选择整个文档对象

　　$('#myId') //选择ID为myId的网页元素

　　$('div.myClass') // 选择class为myClass的div元素

　　$('input[name=first]') // 选择name属性等于first的input元素

2.jQuery特有表达式；
   $('a:first') //选择网页中第一个a元素

　　$('tr:odd') //选择表格的奇数行

　　$('#myForm :input') // 选择表单中的input元素

　　$('div:visible') //选择可见的div元素

　　$('div:gt(2)') // 选择所有的div元素，除了前三个

　　$('div:animated') // 选择当前处于动画状态的div元素
```

***

## 链式操作

jQuery秉承着**写更少的代码，做更多的事情**这个原则和思想，链式操作这种精简代码的形式也应运而生。
链式操作就是选中网页元素后可以对他进行一系列操作，并且所有操作都可以连接在一起，以一个链条的形式写出来，例如如下所示：

```js
$(`#demo`).find(`.h2`).eq(2).html(`Hello`);
```

将其拆解开就是如下所示的含义：

```js
$(`#demo`)//找到id名为demo的所有元素
.find(`.h2`)//再找到其中class名为h2的所有元素
.ep(2)//选择低2个h2元素
.html(`Hello`)；//将其内容改为Hello
```

这是jQuery最令人称道、最方便的特点。它的原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。

同时jQuery还提供了.end()方法，使得结果集可以后退一步：

```js
$(`#demo`).find(`.h2`).eq(2).html(`Hello`)
.end()//退回到选中所有class名为h2的那一步
.ep(0)//选中其中第一个class名为h2的元素
.html(`World`);//将其内容改为World
```

***

## jQuery创建和移动元素

创建新元素的方法非常简单，只要把新元素直接传入jQuery的构造函数就行了：

```js
　　$('<p>Hello</p>');

　　$('<li class="new">new list item</li>');

　　$('ul').append('<li>list item</li>');
```

**另外**，<br>
复制元素使用.clone()。

删除元素使用.remove()和.detach()。两者的区别在于，前者不保留被删除元素的事件，后者保留，有利于重新插入文档时使用。

清空元素内容（但是不删除该元素）使用.empty()。

关于**移动元素**，jQuery提供了两组方法去操作元素在网页中的位置移动。一是直接移动该元素，二是移动其他元素使目标元素到预期位置为止。

如下所示：

```js
$('div').insertAfter($('p'));//将div元素移动到p元素后面。

$('p').after($('div'));//将p元素加到div元素前面。
```

表面上看，这两种方法的效果是一样的，唯一的不同似乎只是操作视角的不同。但是实际上，它们有一个重大差别，那就是返回的元素不一样。第一种方法返回div元素，第二种方法返回p元素。你可以根据需要，选择到底使用哪一种方法。

使用这种模式的操作方法，一共有四对：
>.insertAfter()和.after()：在现存元素的外部，从后面插入元素<br>
>.insertBefore()和.before()：在现存元素的外部，从前面插入元素<br>
>.appendTo()和.append()：在现存元素的内部，从后面插入元素<br>
>.prependTo()和.prepend()：在现存元素的内部，从前面插入元素<br>

***

## jQuery修改元素属性

jQuery中使用attr()方法来获取和设置元素属性,attr是attribute（属性）的缩写,是js中setAttribute()和getAttribute()的简化

最基本常用的用法:

```js
$(`img`).attr(`src`,`img/a.jpg`);
$(`img`).attr(`width`,`100px`);
```

attr()一般有四种用法，如下所示：

```js
$(selector).attr(attribute) //返回被选元素的属性值
$(selector).attr(attribute,value)//设置被选元素的属性和属性值。
$(selector).attr(attribute,function(index,oldvalue))//用函数返回值设置被选元素的属性和值。
$(selector).attr({attribute:value,attribute:value...})//为被选的许多元素设置属性和值。
```

另外，还有如下两个修改属性的操作：

```js
$(`div`).add(selector)//在div元素中添加选择器中的内容，内容可以时字符串、一个或多个元素集合、html片段等。
$(`div`).addClass(className)//在div元素的类名中添加className包含的内容。
```
