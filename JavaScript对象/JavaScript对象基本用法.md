# JS对象基本用法

### 徐上博

<br>

**对象的本质：**

1. *无序的数据集合；*
2. *键值对的集合。*

***
<ul>
  <li><a href="#one">声明对象</a></li>
  <li><a href="#two">删除操作</a></li>
  <li><a href="#three">查询操作</a></li>
  <li><a href="#four">修改与增加操作</a></li>
  <li><a href="#five">关于判断属性是否在项目中的操作以及这些操作的区别</a></li>
</ul>

***

<h2 id="one">声明对象</h2>

两种主要声明方式：

   1. `let obj={'xxx':'aaa','yyy':20}`
   2. `let obj=new Object({'xxx':'aaa','yyy':20})`
<br>

**注**：上述中，1是2的简便写法，2是正规写法。<br>

除两种主要声明方式外，还有一种声明无名对象的写法：<br>
`console.log({'xxx':'aaa','yyy':20})`

**有以下几点需要注意：**

* 键名（属性名）是字符串，不是标识符，可以包含任意字符；
* 属性名引号可以省略，但省略后就需要按照写标识符的规则来写属性名或者写数字；
* 即便是引号省略了按照标识符的规则命名的属性名，**它也依旧是字符串**。

**隐藏属性**：JS每个对象都有一个隐藏属性，其中都储存着指向原型（可以理解为共有属性）的地址。<br>
>原型也是一个对象，所有对象的原型叫做根对象，其隐藏属性为null。

***

<h2 id="two">删除操作</h2>

* `delete obj.xxx`<br>
* `delete obj['xxx']`<br>
两者等价，表示删除属性xxx的一切，即删除属性名与属性值。<br>
<br>

一个属于改写操作的“删除”：<br>
* `obj.xxx=undefined`<br>
将属性值变成undefined，其属性名不变。

***

<h2 id="three">查询操作</h2>
<br>

**查询属性**：

* `Object.keys(obj)`：查看对象的所有自身属性。
* `console.dir(obj)`：查看对象的所有自身以及隐藏属性。
* `obj.hasOwnProperty('toString')`：查询*toString*是否是自身属性。若是则返回*true*，不是则返回*false*。

**查询属性值**

* `obj['xxx']`：查看xxx属性的属性值；
* `obj.xxx`：查看xxx属性的属性值；
* `obj[xxx]`：查看变量xxx对应字符串的属性值（如果有的话）。

***

<h2 id="four">修改与增加操作</h2>

1. 直接赋值
   * `let obj={'xxx':'aaa'}`
   * `obj.xxx='aaa'` <=等价于=> `obj['xxx']='aaa'`
   * `obj.['x'+'xx']='aaa'`
   * `let key = 'xxx' ` `obj[key]='aaa'`
  
2. 批量赋值<br>
   `Object.assign(obj,{'xxx':'aaa','yyy':20})`<br>
   其中`obj`代表项目名称，`{}`内的内容代表想要添加的属性内容。

**注意：一般而言，修改对象属性时若涉及到隐藏属性的内容时，一般只会在本对象内添加一个修改后隐藏属性的内容，原型不会受到影响。但要修改原型也有办法，不过一般不推荐这么做，会出许多问题。**

修改对象隐藏属性（*以`__proto__`为隐藏属性名称的对象举例*）：<br>
1. `obj.__proto__.toString='xxx'`<br>
将obj的原型toString内容修改为'xxx'。
2. `obj.__proto__=null`<br>
使用后，obj就不再拥有隐藏属性。
3. `obj.__proto__=obj2`
将obj的原型替换为对象obj2。

**一般而言，在修改原型时不推荐用带有类似__proto__的语句，建议改用如下的语句：**
```JavaScript
//Object.create
let obj=Object.create(obj2)
//创建一个空对象obj，其原型为obj2
obj.name='jack'
//为对象obj增加一个属性'name',属性值为'jack'；用增、改的操作来为对象增加内容。
```

***

<h2 id="five" style="font-size:18px">关于判断属性是否在项目中的操作以及这些操作的区别</h2>

* 判断对象中是否含有某个属性：<br>
`'xxx' in obj`；返回true则在，返回false则不在。
* 含有某个属性名且属性值为undefined：<br>
`'xxx' in obj && obj.xxx === undefined`<br>
返回true/false
* 判断某属性是自身属性还是隐藏属性：
`obj.hasOwnProperty('xxx')`<br>
返回true表示是自身属性，返回false则表示属性不存在或者属性是隐藏属性。

**注意`'xxx' in obj`和`obj.hasOwnProperty('xxx')`的区别**：<br>

* 前者专注于判断属性是否存在，不论其是自身属性还是隐藏属性。
* 后者则用于判断属性是否是自身属性，不存在或者是隐藏属性时都返回false。
* 两者合用可以用于判断属性是否是隐藏属性：<br>
`'xxx' in obj && obj.hasOwnProperty('xxx')`
