GitHub排版教程  
====

## 大标题测试  
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓  
大标题测试  
====  
↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑
规范的README文件开头都写上一个标题，这被称为大标题。  
在文本下面加上 `=` ，那么上方的文本就变成了大标题。等于号的个数无限制，但一定要大于0个。。。  
比大标题低一级的是中标题，也就是显示出来比大标题小点。  

中标题    
------
在文本下面加上 下划线 - ，那么上方的文本就变成了中标题，同样的 下划线个数无限制。  
除此之外，你也会发现大，中标题下面都有一条横线，没错这就是 = 和 - 的显示结果。

如果你只输入了等于号=，但其上方无文字，那么就只会显示一条直线。如果上方有了文字，  
但你又只想显示一条横线，而不想把上方的文字转义成大标题的话，那么你就要在等于号=和文字直接补一个空行。  
-
## 补空行  
`补空行：是很常用的用法，当你不想上下两个不同的布局方式交错到一起的时候，就要在两种布局之间补一个空行。`  
如果你只输入了短横线（减号）-，其上方无文字，那么要显示直线，必须要写三个减号以上。  
不过与等于号的显示效果不同，它显示出来时虚线而不是实线。

同减号作用相同的还有星号*和下划线_，同样的这两者符号也要写三个以上才能显示一条虚横线。  

除此以外，关于标题还有等级表示法，分为六个等级，显示的文本大小依次减小。  
不同等级之间是以井号，1-6级(个)；  
# 一级标题  
## 二级标题  
### 三级标题  
#### 四级标题  
##### 五级标题  
###### 六级标题  
`大标题大小和一级标题相同，中标题大小和二级标题相同。`

## 普通文本  
直接输入的文字就是普通文本。  
需要注意的是要换行的时候不能直接通过回车来换行，需要使用`<br>(或者<br/>)`。 

也就是html里面的标签。事实上，markdown支持一些html标签，你可以试试。  
当然如果你完全使用html来写的话，就丧失意义了，毕竟markdown并非专门做前端的，  

然而仅实现一般效果的话，它会比html写起来要简洁得多得多啦。  
此外，要显示一个超链接的话，就直接输入这个链接的URL就好了。显示出来会自动变成可链接的形式的

## 单行文本  
使用两个Tab符实现单行文本。  

## 多行文本  
多行文本和单行文本稍微差别，只要在每行行首加两个Tab  

## 部分文字的高亮  
如果你想使一段话中部分文字高亮显示，来起到突出强调的作用，那么可以把它用 `Tab键上的一个符号` 包围起来。  
注意这不是单引号，而是Tab上方，数字1左边的按键（注意使用英文输入法）。  
Thank `You` . Please `Call` Me `Coder`  

## 文字超链接  
给一段文字加入超链接的格式是这样的 [ 要显示的文字 ]( 链接的地址 )。比如：  
[我的主页](https://github.com/KissMyLady)  

你还可以给他加上一个鼠标悬停显示的文本。
[我的主页](https://github.com/KissMyLady"悬停显示")  

## 插入符号  
圆点符：星号(小键盘的那个)    
* 昵称：流浪苍穹  
* 别名：歌者  
* 中文名：执剑人    

此外还有二级圆点和三级圆点。就是多加一个Tab(空格)。  
* 编程语言  
    * 胶水语言  
        * Python  

如果你觉得三级的结构还不够表达清楚的话，我们可以试着换一种形式，`请看字符包围`。  

## 缩进  
>数据结构  
>>二叉树  
>>>三叉树  
>>>>四叉树  
>>>>>五叉树 

使用大于号实现此功能, 里面的大于号分别是：(1, 2, 3, 4, 5)。  

## 图片URL链接(导入)  
叹号! + 方括号[ ] + 括号( ) 其中叹号里是图片的URL  

## GitHub仓库里的图片  
在仓库里面上传图片，应用仓库图片url地址就可以了。  

## 给图片加上超链接  
嵌套写法  
[![baidu]](http://baidu.com)  
[baidu]:http://www.baidu.com/img/bdlogo.gif "百度Logo"  
这两句和前面的写法差异较大，但是也极易模仿着写出，就不过多介绍了。  
只需注意上下文中的 baidu 是你自己起的标识的名称，可以随意，但是一定要保证上下两行的 标识 是一致的。  
这样就能实现 点击图片进入网页的功能了。  

## 插入代码片段  
使用tab上面的\`\， 像这样：  
```Python
import this 

The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!

```



 
 
