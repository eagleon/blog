Markdown: Syntax
================
* [概述]（＃概述）
    * [哲学]（＃哲学）
    * [行内HTML]（＃HTML）
    * [特殊字元自动转换]（＃autoescape）
* [区块元素]（＃地块）
    * [段落和换速行]（＃P）
    * [标题]（＃头）
    * [区块引言]（引用文字）
    * [清单]（＃列表）
    * [程式码区块]（＃precode）
    * [分隔线]（＃HR）
* [区段元素]（＃跨度）
    * [连结]（＃链接）
    * [强调]（＃EM）
    * [程式码]（＃代码）
    * [图片]（＃图）
* [其它]（＃杂项）
    * [跳脱字元]（＃反斜线）
    * [自动连结]（＃自动连结）
* [感谢]（＃确认）

**注意：**这份文件是用降价写的，你可以[看看它的原始档] [SRC]。

  [SRC]：https://github.com/othree/markdown-syntax-zhtw/blob/master/syntax.md

* * *

<h2 id="overview">概述</ H2>

<h3 id="philosophy">哲学</ H3>

降价的目标是实现“易读易写”。

不过最需要强调的便是它的可读性。一份使用降价语法受到一些既有文本到HTML的格式的影响，包括[Setext] [1]，[ATX] [2]，[纺织] [3]，[reStructuredText的] [4]，[Grutatext] [5]和[EtText] [6]，然而眼霜灵感来源其实是纯文字的电子邮件格式。

  [1]：http://docutils.sourceforge.net/mirror/setext.html
  [2]：http://www.aaronsw.com/2002/atx/
  [3]：http://textism.com/tool​​s/textile/
  [4]：http://docutils.sourceforge.net/rst.html
  [5]：http://www.triptico.com/software/grutatxt.html
  [6]：http://ettext.taint.org/doc/

因此降价

<h3 id="html">行内HTML </ H3>

降价的语法有个主要的目的：用来作为一种网路内容的*写作*用语言。

降价不是要来取代HTML，甚至也没有要和它相似，它的语法种类不多，只和HTML的一部分有关系，重点*不是*要创造一种更容易写作的HTML文件的语法，我认为的HTML已经很容易写了，降价的重点在于，它能让文件更容易阅读，编写，HTML是一种*发布*的格式，降价是一种*编写*的格式，因此，降价的格式语法只涵盖纯文字可以涵盖的范围。

不在降价涵盖范围之外的标签，都可以直接在文件里面用的HTML撰写不需要额外标注这是HTML或是降价，只要直接加标签就可以了。

只有区块元素──比如`<DIV>`，`<TABLE>`，`<PRE>`，`<P>`标签或是空白来缩排。降价的产生器有智慧型判断，可以避免在区块标签前后加上没有必要的`<P>`标签。

举例来说，在降价文件里加上一段HTML的表格：

    这是一个普通的段落。

    <TABLE>
        <TR>
            <TD>富</ TD>
        </ TR>
    </ TABLE>

    这是另一个经常段。

请注意，降价语法在HTML的区块标签中将不会被进行处理。例如，你无法在HTML的区块内使用降价形式的`*强调*`。

HTML的区段标签如`<SPAN>`，`<CITE>`，`<DEL>`则不受限制，可以在降价的段落，清单或是标题里任意使用。依照个人习惯，甚至可以不用降价格式，而采用的HTML标签来格式化举例说明：如果比较喜欢的HTML的`<A>`或`<IMG>`标签，可以直接使用这些标签，而不用降价提供的数学家或是影像标示语法。

HTML区段标签和区块标签不同，在区段标签的范围内，降价的语法是有效的。

<h3 id="autoescape">特殊字元自动转换</ H3>

在HTML文件中，有两个字元需要特殊处理：`<`和`＆`<`符号用于起始标签，`＆`符号，则用于标记的HTML实体，如果你只是想要使用这些符号，你必须要使用实体的形式，像是`<`和`＆`。

'＆'符号其实很让写作网路文件的人很困扰，如果你要打“AT＆T公司”，你必须要写成“`＆T`”，还得转换网址内的'＆'符号，如果你要连结到：

    http://images.google.com/images?num=30&q=larry+bird

你必须要把网址转成：

    http://images.google.com/images?num=30&q=larry+bird

才能放到连结标签的`HREF`属性里。不用说也知道这很容易忘记，这也可能是HTML的标准检查工程学系检查到的错误中，数量最多的。

降价允许你直接使用这些符号，但是你要小心跳脱字元的使用，如果你是在HTML的实体中使用'＆'符号的话，它不会被转换，而在其它情形下，它则会被转换成`＆`所以你如果要在文件中插入一个著作权的符号，你可以这样写：

    ©

降价将不会对这段文字做修改，但是如果你这样写：

    AT＆T公司

降价就会将它转为：

    AT＆T公司

类似的状况也会发生在'<'符号上，因为降价支援[行内的HTML（HTML），如果你是使用'<'符号作为HTML的标签使用，那降价也不会对它做任何转换，但是如果你是写：

    4 <5

降价将会把它转换为：

    4 <5

不过需要注意的是，代码范围内，不论是行内还是区块，`<`和`＆`两个符号都*一定*会被转换成HTML实体，这项特性让你可以很容易地用降价写HTML代码（和HTML相对而言，HTML的语法中，你要把所有的`<`和`＆`都转换为HTML实体，才能在HTML文件里面写出的HTML代码。）

* * *

<h2 id="block">区块元素</ H2>


<h3 id="p">段落和换速行</ H3>

选项​​卡，则该行也会被视为空行），一般的段落不需要用空白或断行缩排。

“一个以上相连接的行句组成的”这句话其实暗示了降价允许段落内的强迫断行，这个特性和其他大部分的文本到HTML的格式不一样（包括MovableType的“转换断行”选项），其它的格式会把每个断行都转成`<br />`标签。

如果你真的*想要插入`<br />`标签的话，在行尾加上两个以上的空白，然后按ENTER键。

是的，这确实需要花比较多功夫来插入`<br />`，但是“每个换速行都转换为`<br />`”的方法在降价中并不适合，降价中的电子邮件式的[区块引言] [BQ]和多段落的[清单] [1]在使用换速行来排版的时候，不但更好用，还更好阅读。

  [BQ]：＃大段引用。
  [1]：＃列表

<h3 id="header">标题</ H3>

降价支援两种标题的语法，[Setext] [1]和[ATX] [2]形式。

Setext形式是用底线的形式，利用`=`（最低速度高阶标题）和` - `（第二阶标题），例如：

    这是一个H1
    =============

    这是一个H2
    -------------

任何数量的`=`和` - `都可以有效果。

ATX形式，则是在行首插入1到6个`＃`，对应到标题1到6阶，例如：

    ＃这是一个H1

    ＃＃这是一个H2

    ######这是一个H6

你可以选择性地“关闭”ATX `＃`，τ行尾的`＃`数量也不用和开头一样（行首的井字数量决定标题的阶数）：

    ＃这是一个H1＃

    ＃＃这是一个H2＃

    ＃＃＃这是一个H3 ######


<h3 id="blockquote"> Blockquotes </ H3>

降价使用电子邮件形式的区块引言，如果你很熟悉如何在电子邮件信件中引言，你就知道怎么在降价`>`：

    >这是一个大段引用两段。 Lorem ipsum悲坐在阿梅特
    > consectetuer adipiscing ELIT。 Aliquam hendrerit MI posuere lectus。
    >前庭enim wisi，灵猫NEC，fringilla中，laoreet简历，risus。
    >
    > Donec坐在阿梅特nisl。 Aliquam SEMPER ipsum坐在阿梅特velit。 Suspendisse
    > ID SEM consectetuer的Libero luctus adipiscing。

降价也允许你只在整个段落的第一行最前面加上`>`：

    >这是一个大段引用两段。 Lorem ipsum悲坐在阿梅特
    consectetuer adipiscing ELIT。 Aliquam hendrerit MI posuere lectus。
    前庭enim wisi，灵猫NEC，fringilla在laoreet简历，risus。

    > Donec坐在阿梅特nisl。 Aliquam SEMPER ipsum坐在阿梅特velit。 Suspendisse
    ID SEM consectetuer的Libero luctus adipiscing。

`>`：

    >这是第一个层次的引用。
    >
    >>这是嵌套的大段引用。
    >
    >返回到第一级。

引言的区块内也可以使用其他的降价语法，包括标题，清单，程式码区块等：

>＃＃这是一个头。
>
> 1。这是第一个列表项。
> 2。这是第二个列表项目。
>
>下面是一些示例代码：
>
>返回函数shell_exec（“回声输入| $ markdown_script”）;

任何标准的文字编辑器都能简单地建立电子邮件样式的引言，例如的BBEdit，你可以选取文字后然后从贝壳中选择*增加引言阶层*。

<h3 id="list">清单</ H3>

降价支援有序清单和无序清单。

无序清单使用星号，加号技术或是减号作为清单标记：

    *红
    *绿
    *蓝

等同于：

    +红
    +绿
    +蓝

也等同于：

     - 红
     - 绿色
     - 蓝

有序清单则使用数字接着一个英文句点：

    1。禽流
    2。麦克海尔
    3。教区

很重要的一点是，你在清单标记上使用的数字并不会影响; output的HTML的结果，上面的清单工程学系产生的HTML标记为：

    <OL>
    <LI>鸟</ LI>
    <LI>麦克海尔</ LI>
    <LI>教区</ LI>
    </ OL>

如果你的清单标记写成：

    1。禽流
    1。麦克海尔
    1。教区

或什至是：

    3。禽流
    1。麦克海尔
    8。教区

你都会得到完全相同的HTML的输出。重点在于，你可以让降价

如果你使用懒惰的写法，建议第一个项目最好还是从1。开始，因为降价未来可能会支援有序清单的启动属性。

标签。

要让清单看起来更漂亮，你可以把来源用固定的缩排整理好：

    * Lorem ipsum悲坐在阿梅特，consectetuer adipiscing ELIT。
        Aliquam hendrerit MI posuere lectus。前庭enim wisi
        灵猫NEC，fringilla在laoreet简历，risus。
    * Donec坐在阿梅特nisl。 Aliquam SEMPER ipsum坐在阿梅特velit。
        Suspendisse ID SEM consectetuer的Libero luctus adipiscing。

但是如果你很懒，那也不一定需要：

    * Lorem ipsum悲坐在阿梅特，consectetuer adipiscing ELIT。
    Aliquam hendrerit MI posuere lectus。前庭enim wisi
    灵猫NEC，fringilla在laoreet简历，risus。
    * Donec坐在阿梅特nisl。 Aliquam SEMPER ipsum坐在阿梅特velit。
    Suspendisse ID SEM consectetuer的Libero luctus adipiscing。

如果清单项目间用空行分开，降价会把项目的内容在; output时用`<P>`
标签包起来，举例来说：

    *鸟
    *魔术

会被转换为：

    <UL>
    <LI>鸟</ LI>
    <LI>魔术</ LI>
    </ UL>

但是这个：

    *鸟

    *魔术

会被转换为：

    <UL>
    <LI>鸟</ P> </ LI>
    <LI>魔术</ P> </ LI>
    </ UL>

清单项目可以包含多个段落，每个项目下的段落都必须缩排4个空白或是一个选项卡：

    1。这是一个两段的列表项。 Lorem ipsum悲
        坐在阿梅特，consectetuer adipiscing ELIT。 Aliquam hendrerit
        MI posuere lectus。

        前庭enim wisi，灵猫NEC，fringilla中，laoreet
        简历，risus。 Donec坐在阿梅特nisl。 Aliquam SEMPER ipsum
        坐阿梅特velit。

    2。 Suspendisse ID SEM consectetuer的Libero luctus adipiscing。

也允许：

    *这是一个两段的列表项。

        这是列表中的项目的第二段。你
    只需要缩进的第一行。 Lorem ipsum悲
    坐在阿梅特，consectetuer adipiscing ELIT。

    *在同一列表中的另一个项目。

如果要在清单项目内放进引言，那`>`就需要缩排：

    *一个大段引用的列表项：

        >这是一个大段引用
        >里面的列表项。

如果要放程式码区块的话，该区块就需要缩排*两次*，也就是8个空白或是两个选项卡：

    *一个代码块的列表项：

            <code去here>


当然，项目清单很可能会不小心产生，像是下面这样的写法：

    1986年。一个伟大的赛季。



    1986 \。一个伟大的赛季。

<h3 id="precode">程式码区块</ H3>

会用`<PRE>`和`<CODE>`标签来把程式码区块包起来。

要在降价中建立程式码区块很简单，只要简单地缩排4个空白或是1个选项卡就可以，例如，下面的input;：

    这是一个普通的段落：

        这是一个代码块。

降价会转换成：

    <p>这是一个普通的段落：</ P>

    <PRE>的<code>这是一个代码块。
    </ CODE> </ PRE>

这个每行一阶的缩排（4个空白或是1个选项卡），都会被移除，例如：

    下面是一个AppleScript的例子：

        告诉应用程序的“富”
            嘟
        年底告诉

会被转换为：

    <p>下面是一个AppleScript的例子：</ P>

    <PRE>的<code>告诉应用程序的“富”
        嘟
    年底告诉
    </ CODE> </ PRE>

一个程式码区块会一直持续到没有缩排的那一行（或是文件结尾）。

在程式码区块里面，`＆`，`<`和`>`会自动转成HTML的实体，这样的方式让你非常容易使用降价插入范例用的HTML原始码，只需要复制贴上，再加上缩排就可以了，剩下的降价都会帮你处理，例如：

        <div class="footer">
            © 2004年美孚公司
        </ DIV>

会被转换为：

    <PRE>的<code> <div class="footer">
        &COPY; 2004美孚公司
    </ DIV>
    </ CODE> </ PRE>

程式码区块中，一般的降价语法不​​会被转换，像是星号技术叧只是星号，这表示你可以很容易地以降价语法撰写降价语法相关的文件。

<h3 id="hr">分隔线</ H3>



    * * *

    ***

    *****

     - - - 

    ---------------------------------------


* * *

<h2 id="span">区段元素</ H2>

<h3 id="link">连结</ H3>

降价支援两种形式的数学家语法：*行内*和*参考*两种形式。

不管是哪一种，香港公共图书馆 - 的文字都是用[方括号]来标记。

标题文字，只要在网址后面，用双引号把标题文字包起来即可，例如：

    这就是一个例子]（http://example.com/“标题”）内嵌链接。

    [链接]（http://example.net/）有没有title属性。

会产生：

    <p>这是<a href="http://example.com/" title="Title">
    一个例子</ A>内嵌链接。</ P>

    <P> <a href="http://example.net/">此链接</ A>
    title属性。</ P>

如果你是要连结到同样主机的资源，你可以使用相对路径：

    详情请参阅我的[关于]（/）/约页。



    这是一个例子] [ID]引用样式的链接。

你也可以选择性地在两个方括号中间加上空白：

    这是一个例子] [ID]引用样式的链接。

接着，在文件的任意处，你可以把这个标签的数学家来源订出来：

    [ID]：http://example.com/“可选的标题在这里”

连结定义的形式为：

*方括号，里面input;香港公共图书馆 - 的辨识用标签
*接着一个冒号
*接着一个以上的空白或选项卡
*接着连结的网址
*选择性地接着标题内容，可以用单引号，双引号或是括弧包着

下面这三种连结的定义都是相同：

[富]：http://example.com/“可选的标题在这里”
[富]：http://example.com/“可选的标题下面”
[富]：http://example.com/（可选的标题在这里）

**请注意：**有一个已知的问题是Markdown.pl 1.0.1会忽略单引号包起来的数学家称号。

香港公共图书馆 - 网址也可以用方括号包起来：

    [编号]：<http://example.com/>“可选的标题在这里”

你也可以把属性放到下一行，也可以加一些缩排，网址太长的话，这样会比较好看：

    [编号]：http://example.com/longish/path/to/resource/here
        “可选的标题在这里”

网址定义只有在产生连结的时候用到，并不会直接出现在文件之中。



[链接文字] [A]
[链接文字] [甲]

“谷歌”香港公共图书馆 - 到google.com的，你可以简化成：

[谷歌] []

然后定义连结内容：

[谷歌]：http://google.com/

由于连结文字可能包含空白，所以这种简化的标签内也可以包含多个文字：

[]有关详细信息，请访问[Daring Fireball的。

然后接着定义连结：

[Daring Fireball的]：http://daringfireball.net/



下面是一个参考式连结的范例：

    我得到的10倍以上[谷歌] [1]比从交通
    [雅虎] [2]或[MSN] [3]。

      [1]：http://google.com/“谷歌”
      [2]：http://search.yahoo.com/“雅虎搜索”
      [3]：http://search.msn.com/“MSN搜索”

如果改成用连结名称的方式写：

    我得到从[] []比10倍以上的流量
    [雅虎] []或[MSN] []。

      [谷歌]：http://google.com/“谷歌”
      [雅虎]：http://search.yahoo.com/“雅虎搜索”
      [MSN]：http://search.msn.com/“MSN搜索”

上面两种写法都会产生下面的HTML代码。

    <p>我得到的10倍以上的<a href =“htt​​p://google.com/”交通
    TITLE =“谷歌”谷歌</ A>比
    <a href="http://search.yahoo.com/" title="Yahoo Search">雅虎</ A>
    或<a href="http://search.msn.com/" title="MSN Search"> MSN </ A> </ P>

下面是用行内形式写的同样一段内容的降价文件，提供作为比较之用：

    我得到的10倍以上[谷歌]交通（http://google.com/“谷歌”）
    [雅虎]（http://search.yahoo.com/“雅虎搜索”）或比
    [MSN]（http://search.msn.com/“MSN搜索”）。

81个字元，但是用行内形式的数学家却会增加到176个字元，如果是用缃HTML的格式来写，会有234个字元，在HTML格式中，标签比文字还要多。

使用降价

<h3 id="em">强调</ H3>

降价使用星号技术(`*`)和底线(`_`)作为标记强调字词的符号，被'*'或'_'包围的字词会被转成用`<EM>`标签包围，用两个`*`或`_`包起来的话，则会被转成`<STRONG>，例如：

    单星号* * * *

    _single underscores_

    **双星号**

    __double underscores__

会转成：

    的<em>单星号</ EM>

    的<em>单下划线</ EM>

    <STRONG>双星号</ STRONG>

    <STRONG>双下划线</ STRONG>



强调也可以直接差在文字中间：

    UN *该死*可信

但是如果你的`*`和`_`两边都有空白的话，它们就只会被当成普通的符号。

如果要在文字前后直接插入普通的星号或底线，你可以用反斜线：

    \ *这个文本是由字面星号包围\ *

<h3 id="code">程式码</ H3>

如果要标记一小段行内程式码，你可以用反引号把它包起来（`````），例如：

    使用`的printf（）函数。

会产生：

    <p>使用的<code>的printf（）</ code>函数。</ P>



    ``有文字反引号（`）在这里。“

这段语法会产生：

    <P>的<code>有文字的反引号（`）</> </ P>



一个单一的反引号的代码跨度：`````

一个代码跨度反引号分隔的字符串：```富```

会产生：

<p>一个单一代码跨度反引号的<code>`</代码> </ P>

<p>一个代码跨度反引号分隔的字符串：<CODE>的`foo`</代码> </ P>

在程式码区段内，`＆`和方括号都会被转成HTML的实体，这样会比较容易插入的HTML原始码，降价会把下面这段：

    请不要使用任何`<blink>`标签。

转为：

    </ P> <p>请不要使用任何<code> <blink> </ code>标记。

你也可以这样写：

    ` - `是十进制编码相当于` - `。

以产生：

    <P> <CODE> &#8212; </代码>是十进制编码
    相当于<CODE> &mdash; </代码> </ P>



<h3 id="img">图片</ H3>

很明显地，要在纯文字登入中设计一个“自然”的语法来插入图片产品是有一定难度的。

降价使用一种和香港公共图书馆 - 很相似的语法来标记图片产品，同样也允许两种样式：*行内*和*参考*。

行内图片的语法看起来像是：

    [ALT]（/路径/ / img.jpg）

    [文本]（/路径/ / img.jpg“可选的标题”）

详细叙述如下：

*一个惊叹号'！'
*接着一个方括号，里面放上图片产品的替代文字
*接着一个普通括号，里面放上图片产品的网址，最后更新还可以用引号包住并加上
    选择性的“标题”的文字。

参考式的图片产品语法，则长得像这样：

    ！[ALT文本] [ID]

“ID”是图片产品参考的名称，图片产品参考的定义方式，则和香港公共图书馆 - 参考一样：

    [ID]：/ /图像URL“可选的标题属性”

到目前为止，降价还没有办法指定图片产品的宽高，如果你需要的话，你可以使用普通的`<IMG>`标签。

* * *

<h2 id="misc">其它</ H2>

<h3 id="autolink">自动连结</ H3>

降价降价就会自动把它转成香港公共图书馆 - ，香港公共图书馆 - 的文字就和香港公共图书馆 - 位置一样，例如：

    <http://example.com/>
    
降价会转为：

    <a href="http://example.com/"> http://example.com/ </ A>

自动的邮件连结也很类似，只是降价会先做一个编码转换的过程，把文字字元转成16步进位码的HTML实体，这样的格式可以混淆一些不好的信箱地址收集机器人，例如：

    <address@example.com>

降价会转成：

    <A HREF =“MAILTO：addre
    ss@example.co
    M“>地址：EXA
    mple.com </ A>

在浏览器里面，这段字串会变成一个可以点击的“address@example.com”连结。



<h3 id="backslash">跳脱字元</ H3>

降价`的<em>`标签），你可以在星号的前面加上反斜线：

    \ *字面星号\ *

降价支援在下面这些符号前面加上反斜线来帮助插入普通的符号：

    \反斜线
    `反引号
    *星号
     - 底线
    {}大括号
    []方括号
    （）括号
    ＃井字号
+加号
- 减号
    。英文句点
    ！惊叹号

<h2 id="acknowledgement">感谢</ H2>

感谢[leafy7382] []协助翻译，HLB ][],[ Randylien] []帮忙润稿，ethantw] []的[汉字标准格式的CSS复位] []，[WM] []回报文字错误。

[leafy7382]：https://twitter.com/＃/ leafy7382！
[HLB]：http://iamhlb.com/
[Randylien]：http://twitter.com/randylien
[ethantw]：https://twitter.com/＃/ ethantw
[汉字标准格式的CSS重置]：http://ethantw.net/projects/han/
[西马]：http://kidwm.net/
