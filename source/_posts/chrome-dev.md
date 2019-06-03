---
title: chrome控制台不完全指南
date: 2019-05-25 17:25:00
categories: 工具
tags:
 - Chrome
---
# chrome控制台不完全指南

Chrome的开发者工具是个很强大的东西，相信程序员们都不会陌生，不过有些小功能可能并不为大众所知，所以，写下这篇文章罗列一下可能你所不知道的功能，有的功能可能会比较实用，有的则不一定，也欢迎大家补充交流。

话不多话，我们开始。

---

[]()
<a name="42f01000"></a>
## 代码格式化

有很多css/js的代码都会被 minify 掉，你可以点击代码窗口左下角的那个 { } 标签，chrome会帮你给格式化掉。 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/pretty-code.gif#align=left&display=inline&height=319&originHeight=319&originWidth=707&status=done&width=707)

[]()
<a name="c0569357"></a>
## 强制DOM状态

有些HTML的DOM是有状态的，比如`<a>` 标签，其会有 `active`，`hover`， `focus`，`visited`这些状态，有时候，我们的CSS会来定关不同状态的样式，在分析网页查看网页上DOM的CSS样式时，我们可以点击CSS样式上的 `:hov` 这个小按钮来强制这个DOM的状态。 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/state.gif#align=left&display=inline&height=331&originHeight=331&originWidth=853&status=done&width=853)

[]()
<a name="b599979e"></a>
## 动画

现在的网页上都会有一些动画效果。在Chrome的开发者工具中，通过右上角的菜单中的 `More Tools => Animations` 呼出相关的选项卡。于是你就可以慢动作播放动画了（可以点选 `25%` 或 `10%`），然后，Chrome还可以帮你把动画录下来，你可以拉动动再画的过程，甚至可以做一些简单的修改。 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/animation.gif#align=left&display=inline&height=887&originHeight=887&originWidth=542&status=done&width=542)

[]()
<a name="0f9b9760"></a>
## 直接编辑网页

在你的 console 里 输入下面的命令：

```javascript
document.designMode = "on"
```
也可以使用下面的命令

```javascript
document.body.contentEditable=true
```

这样就可以直接修改网页上的内容了。

P.S. 下面这个抓屏中还演示了一个如何清空console的示例。你可以输入 clear() 或是 按 `Ctrl+L`（Windows下），`CMD + K`(Mac下) <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/editor.gif#align=left&display=inline&height=442&originHeight=442&originWidth=1078&status=done&width=1078)

<a name="6zTrS"></a>
## 网页截取长图[]()
按 F12 弹出控制台，按 `ctrl+shift+p` 弹出输入框<br />![无标题.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558621627703-6f3a7a25-13c2-4c5f-9bb1-fa35ededb0d5.png#align=left&display=inline&height=437&name=%E6%97%A0%E6%A0%87%E9%A2%98.png&originHeight=437&originWidth=1397&size=45512&status=done&width=1397)<br />输入full，选择 `capture full size screenshot` 然后点击就会对当前网页进图并生成下载一个图片。

<a name="6e9beb1b"></a>
## 网络限速

你可以设置你的网络的访问速度来模拟一个网络很慢的情况。 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/custom-network-throttling-profiles.gif#align=left&display=inline&height=319&originHeight=319&originWidth=707&status=done&width=707)

[]()
<a name="5dbded51"></a>
## 复制HTTP请求

这个是我很喜欢 的一个功能，你可以在 network选项卡里，点击 XHR 过滤相关的Ajax请求，然后在相关的请求上点鼠标右键，在菜单中选择： `Copy => Copy as cURL`，然后就可以到你的命令行下去 执行 curl 的命令了。这个可以很容易做一些自动化的测试。 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/curl.gif#align=left&display=inline&height=442&originHeight=442&originWidth=1078&status=done&width=1078)

友情提示：这个操作有可能会把你的个人隐私信息复制出去，比如你个人登录后的cookie。

[]()
<a name="16a12a75"></a>
## 抓个带手机的图

这个可能有点无聊了，不过我觉得挺有意思的。

在device显示中，先选择一个手机，然后在右上角选 `Show Device Frame`，然后你就看到手机的样子了，然后再到那个菜中中选 Capture snapshot，就可以抓下一个有手机样子的截图了。 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/device.gif#align=left&display=inline&height=532&originHeight=532&originWidth=921&status=done&width=921)<br />
我抓的图如下（当然，不是所有的手机都有frame的） <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/coolshell.cn-iPhone-6-Plus-1-148x300.png#align=left&display=inline&height=300&originHeight=300&originWidth=148&status=done&width=148)

[]()
<a name="1255d2de"></a>
## 设置断点

除了给Javascript的源代码上设置断点调试，你还可以：

[]()
<a name="1dc037c9"></a>
### 给DOM设置断点

选中一个DOM，然后在右键菜单中选 Break on … 你可以看到如下三个选项： <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/break.dom_-768x531.png#align=left&display=inline&height=531&originHeight=531&originWidth=768&status=done&width=768)

[]()
<a name="a1a07c7a"></a>
### 给XHR和Event Lisener设置断点

在 Sources 面页中，你可以看到右边的那堆break points中，除了上面我们说的给DOM设置断点，你还可以给XHR和Event Listener设置断点，载图如下： <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/breakpoints-768x943.png#align=left&display=inline&height=943&originHeight=943&originWidth=768&status=done&width=768)

[]()
<a name="67af05b3"></a>
## 关于Console中的技巧
[]()
<a name="9bdbe234"></a>
### DOM操作

- chrome会帮你buffer 5个你查看过的DOM对象，你可以直接在Console中用 `$0, $1, $2, $3, $4`来访问。
- 你还可以使用像jQuery那样的语法来获得DOM对象，如：`$("#mydiv")`
- 你还可使用 `$$(".class")` 来选择所有满足条件的DOM对象。
- 你可以使用 `getEventListeners($("selector"))` 来查看某个DOM对象上的事件(以数组对象的格式返回)（如下图所示）。

![events-geteventlisteners_expanded.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558622044203-fb5c6bc6-e0b8-4028-ae70-025a3ed4a768.png#align=left&display=inline&height=260&name=events-geteventlisteners_expanded.png&originHeight=293&originWidth=842&size=20037&status=done&width=746)

- 你还可以使用 `monitorEvents($("selector"))` 来监控相关的事件。比如：`monitorEvents(document.body, "click");`

![monitor-events-1024x378.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558622139686-13aca770-cefb-45ba-8f0e-c84bf8f80af0.png#align=left&display=inline&height=378&name=monitor-events-1024x378.png&originHeight=378&originWidth=1024&size=259556&status=done&width=1024)

- monitorEvents($('selector')) 会监测某个元素上绑定的所有事件，一旦该元素的某个事件被触发就会在控制台里显示出来。
- monitorEvents($('selector'),'eventName') 可以监听某个元素上绑定的具体事件。第二个参数代表事件类型的名称。例如 monitorEvents($('#firstName'),'click') 只监测ID为firstName的元素上的click事件。
- monitorEvents($('selector'),['eventName1','eventName3',….]) 同上。可以同时检测具体指定的多个事件类型。
- unmonitorEvents($('selector')) 用来停止对某个元素的事件监测。
<a name="c80e2d88"></a>
### Console中的一些函数

1. monitor函数 & unmonitor<br />
使用 monitor函数来监控一函数，如下面的示例 <br />
![](http://coolshell.cn//wp-content/uploads/2017/01/monitor-604x226.png#align=left&display=inline&height=226&originHeight=226&originWidth=604&status=done&width=604)

unmonitor(function)便是用来停止这一监听.

2. copy函数 

通过此命令可以将在控制台获取到的内容复制到剪贴板。<br />![chrome copy.jpg](https://cdn.nlark.com/yuque/0/2019/jpeg/352947/1558622456186-7666e4ba-5161-4b7a-91f9-ac0e6b397ebd.jpeg#align=left&display=inline&height=203&name=chrome%20copy.jpg&originHeight=203&originWidth=646&size=38170&status=done&width=646)

3. inspect函数 

inspect函数可以让你控制台跳到你需要查看的对象上。如： 

```javascript
inspect(document.body);
```

![](http://coolshell.cn//wp-content/uploads/2017/01/inspect-1024x459.png#align=left&display=inline&height=459&originHeight=459&originWidth=1024&status=done&width=1024)

4. 获取dom元素

要是你用过两天jQuery的话，一定对 `$('.className')` 或者 `$('#id')`  这种选择器不会陌生。上面这俩货分别是jQuery的类选择器和ID选择器。

在一个网页没有引入jQuery的情况下，在控制台里你也可以通过类似的方法选取DOM.

不管 `$('tagName')`  / `$('.class')` / `$('#id')`  还是 `$('.class #id')`  等类似的选择器，都相当于原生JS的 `document.querySelector('')`  方法。这个方法返回第一个匹配选择规则的DOM元素。

在Chrome的控制台里，你可以通过 `$$('tagName')`  或者 `$$('.className')`  记得是两个$$符号来选择所有匹配规则的DOM元素。选择返回的结果是一个数组，可以通过数组的方法来访问其中的单个元素。

看一个案例:

```javascript
   var images = $$('img');
    for (each in images) {
        console.log(images[each].src);
    }
```

![all-selector.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558623195083-4e9ec4ca-c0a6-417f-9e47-5101e3199676.png#align=left&display=inline&height=1500&name=all-selector.png&originHeight=1500&originWidth=2240&size=116682&status=done&width=2240)


更多的函数请参数官方文档 – [Using the Console / Command Line Reference](https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference)

[]()
<a name="a6fb5c4e"></a>
### Console的输出

我们知道，除了`console.log`之外，还有`console.debug`，`console.info`，`console.warn`，`console.error`这些不同级别的输出。另外一个鲜为人知的功能是，`console.log`中，你还可以对输出的文本加上css的样式，如下所示：

```
console.log("%c左耳朵", "font-size:90px;color:#888")
```


![](http://coolshell.cn//wp-content/uploads/2017/01/console.log_-604x185.png#align=left&display=inline&height=185&originHeight=185&originWidth=604&status=done&width=604) <br />
于是，你可以定义一些相关的log函数，如：

```javascript
console.todo = function( msg){console.log( '%c%s %s %s', 'font-size:20px; color:yellow; background-color: blue;', '--', msg, '--');console.important = function( msg){console.log( '%c%s %s %s', 'font-size:20px; color:brown; font-weight: bold; text-decoration: underline;', '--', msg, '--');
```


![](http://coolshell.cn//wp-content/uploads/2017/01/console.log2_-768x309.png#align=left&display=inline&height=309&originHeight=309&originWidth=768&status=done&width=768)

关于console.log中的格式化，你可以参看如下表格：

| **指示符** | **输出** |
| :---: | :---: |
| %s | 格式化输出一个字符串变量 |
| %i or %d | 格式化输出一个整型变量的值 |
| %f | 格式化输出一个浮点数变量的值。 |
| %o | 格式化输出一个DOM对象 |
| %O | 格式化输出一个Javascript对象 |
| %c | 为后面的字符串加上CSS样式 |

除了console.log打印js的数组，你还可以使用console.table来打印，如下所示：

```javascript
var pets = [
  { animal: 'Horse', name: 'Pony', age: 23 },
  { animal: 'Dog', name: 'Snoopy', age: 13 },
  { animal: 'Cat', name: 'Tom', age: 18 },
  { animal: 'Mouse', name: 'Jerry', age: 12}
];
console.table(pets)
```


![](http://coolshell.cn//wp-content/uploads/2017/01/console.table_-768x328.png#align=left&display=inline&height=328&originHeight=328&originWidth=768&status=done&width=768)

[]()
<a name="3280e5b2"></a>
## 关于console对象

console对象除了上面的打日志的功能，其还有很多功能，比如：

- console.trace() 可以打出js的函数调用栈
- console.dir() 将DOM结点以JavaScript对象的形式输出到控制台

![console dir.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558624700975-4de5699f-0919-4975-80fd-e6bba719f821.png#align=left&display=inline&height=382&name=console%20dir.png&originHeight=382&originWidth=1249&size=50800&status=done&width=1249)

- console.time() 和 console.timeEnd() 可以帮你计算一段代码间消耗的时间。

```javascript
console.time("Array initialize");
var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
    array[i] = new Object();
};
console.timeEnd("Array initialize");
```

![console time.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558624794096-0cd27c3a-c697-4abb-a0a9-3a21a3813fe0.png#align=left&display=inline&height=305&name=console%20time.png&originHeight=305&originWidth=1052&size=26450&status=done&width=1052)
- console.group(label)和console.groupEnd(label)  分类管理console的信息，适合于在开发一个规模很大模块很多很复杂的Web APP时，将各自的log信息分组到以各自命名空间为名称的组里面。

![console group.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558624267701-66b475cb-61ad-4906-af41-befa2926ffe2.png#align=left&display=inline&height=386&name=console%20group.png&originHeight=386&originWidth=1138&size=31475&status=done&width=1138)

- console.profile() 和 console.profileEnd() 可以让你查看CPU的消耗。
- console.count() 可以让你看到相同的日志当前被打印的次数。

![console count.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558624554167-f08fb264-9cf1-44de-987f-9920559edf03.png#align=left&display=inline&height=401&name=console%20count.png&originHeight=401&originWidth=1282&size=26140&status=done&width=1282)

- console.assert(expression, object) 可以让你assert一个表达式，它会先对传入的表达式进行断言，只有表达式为假时才输出相应信息到控制台

![console assert.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1558624457988-c2e18f34-7b07-43c2-8d0e-af31a2c5cfe8.png#align=left&display=inline&height=324&name=console%20assert.png&originHeight=324&originWidth=1263&size=24608&status=done&width=1263)



这些东西都可以看看[Google的Console API的文档。](https://developers.google.com/web/tools/chrome-devtools/console/console-reference)

其实，还有很多东西，你可以参看Google的官方文档 – [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)

[]()
<a name="57069e38"></a>
## 关于快捷键

点击在 DevTools的右上角的那三个坚排的小点，你会看到一个菜单，点选 Shortcuts，你就可以看到所有的快捷键了 <br />
![](https://img-blog.csdn.net/20170216103841932?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZmFjZWtib29r/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast#align=left&display=inline&height=322&originHeight=322&originWidth=1920&status=done&width=1920)<br />
![](http://coolshell.cn//wp-content/uploads/2017/01/shortcuts-1024x466.png#align=left&display=inline&height=466&originHeight=466&originWidth=1024&status=done&width=1024)

如果你知道更多，也欢迎补充！
<a name="uwdOn"></a>
## 感谢

- 来源:[https://blog.csdn.net/ij_fantasy/article/details/80652120](https://blog.csdn.net/ij_fantasy/article/details/80652120) 
- 来源: [https://www.cnblogs.com/Wayou/p/chrome-console-tips-and-tricks.html](https://www.cnblogs.com/Wayou/p/chrome-console-tips-and-tricks.html)
- 来源: [https://www.cnblogs.com/MythLeige/p/6196214.html](https://www.cnblogs.com/MythLeige/p/6196214.html)

根据以上博文进行整理修改，感谢。


