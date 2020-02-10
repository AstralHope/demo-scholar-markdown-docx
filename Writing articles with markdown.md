#利用Markdown书写文章

##序言

由于博客上常常需要引用大量代码，现有的Wordpress插件并不能让人满意，再加上CSDN的文章已经全面使用Markdown书写，便查找了一些资料，发现神器[Pandoc](https://github.com/jgm/pandoc/)支持将Markdown转换为word、pdf等多种格式，与latex的兼容性良好，转换方便，便对查阅对资料进行梳理成文，本文亦采用Markdown书写完成。

> [如何用Markdown写论文？](https://www.jianshu.com/p/b0ac7ae98100)
[BibTeX的使用方法](https://www.jianshu.com/p/b0ac7ae98100)
[Jabref使用](https://www.jianshu.com/p/b0ac7ae98100)
[MarkDown - 语法说明](http://www.markdown.cn/#overview)
[Pandoc中的Markdown语法](https://www.cnblogs.com/baiyangcao/p/pandoc_markdown.html)
[Markdown下LaTeX公式、编号、对齐](https://www.zybuluo.com/fyywy520/note/82980)
[Online LaTeX Equation Editor](http://latex.codecogs.com/eqneditor/editor.php)

##环境的搭建

本文使用的所有软件均为跨平台软件，同时支持Windows、macOS、Linux，以下为需要使用的软件与安装方法，后序示例图为我在macOS上使用的截图

###Atom编辑器
如果仅仅是编辑使用Markdown书写文章，Atom已经能够胜任。[点击下载](https://atom.io/)安装即可。
如果有需要，安装[markdown-preview-enhanced](https://atom.io/packages/markdown-preview-enhanced)扩展可以带来更好的预览体验。安装[simplified-chinese-menu](https://atom.io/packages/simplified-chinese-menu)扩展可以安装使用中文包。
安装方法有两种
1. 打开Preference，选择install搜索对应的扩展包名安装即可，此方法需要较好的网络环境，按Atom的代理设置较为复杂，笔者直接在路由器上设置代理才成功完成安装。
2. 点击上方链接下载扩展包解压后移动到`~/.atom/packages`目录即可。

如果你不需要Markdown到Docx的转换、脚注、题注、尾注等功能，到这里便已经结束了，后续软件无需安装。

###python
macOS（成文时最新为10.15.3版本）自带python2.7，可跳过此步，有需要的同学也可以手动安装python3和pip3，若使用`brew install python3`安装会顺带安装pip3，如果使用自带的python2.7，使用`sudo easy_install pip`即可完成pip2的安装。使用python3和pip3的情况下注意自行修改环境变量设置或将`pip`和`python`替换为`pip3`和`python3`。个人习惯于尽可能使用homebrew安装，便于安装和卸载。
其他操作系统按照对应的方法安装好python环境和pip即可，版本不限。
当然也可以选择使用[Anaconda](https://www.anaconda.com/distribution/)套件完成安装。

###Pandoc
Pandoc是一款非常强大的工具，支持Markdown, Docx, PDF, LaTeX, ePub, HTML等常见发布格式的文档处理，参考文献中有提到另一篇[如何把思维导图秒变成幻灯](https://www.jianshu.com/p/f274cad20914)的文章，有需要的同学可以参考学习，后文也只是使用了极少的功能将Markdown转换符合对应标准的Docx文件，更多用法需自行学习探索。
安装方法：直接[点击下载](https://github.com/jgm/pandoc/releases)安装，也可以使用homebrew安装。
安装完后使用`pip install pandoc-fignos`安装`pandoc-fignos`用于图片引用时的转换。不过笔者在使用最新版的Pandoc时遇到了一些问题，切回旧版本才解决，可能是`pandoc-fignos`未更新的问题。

<center><img style="border-radius: 0.3125em;box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);"src="https://gitee.com/Astral/img/raw/master/blog/JabRef.png"><br><div style="border-bottom: 1px solid #d9d9d9;display: inline-block;color: #999;padding: 2px;">高版本pandoc使用pandoc-fignos报错</div>
</center>

###JabRef
[JabRef](https://www.fosshub.com/JabRef.html)是一款文献管理工具，用于记录最后需要在参考文献中使用到各项信息，便于参考文献的统一管理和只能编号，导出的BibTeX对Markdown和Latex的兼容性良好，直接[点击下载](https://www.fosshub.com/JabRef.html)安装即可。

##使用范例
此部分根据[如何用Markdown写论文？](https://www.jianshu.com/p/b0ac7ae98100)改写。
首先下载[demo](https://github.com/AstralHope/demo-scholar-markdown-docx/archive/master.zip)范例并解压。terminal也`cd`到该目录，后文命令均在此目录下执行。该范例中包含了GB/T 7714-2015的规范文件，更多格式的规范可在[citation-style-language](https://github.com/citation-style-language/styles)获取。

###基础使用
使用Atom打开项目文件夹，打开`demo.md`，即可看到一个基础的demo，常规使用Markdown编辑使用即可。右侧如未显示预览，在扩展中开启。
![](https://gitee.com/Astral/img/raw/master/blog/Pandoc-version-bug.png)
demo-math.md中增加了对数学公式对引用，将数学公式用\$公式\$的格式输入即可，\$中为行内公式，\$\$中为单行公式，详细用法参考文章开头的参考文献。
demo-footnote.md中增加了脚注对使用范例，也属于Markdown的常规语法，使用`[^1]`标注即可。
对这类常规对Markdown文档，使用下列格式及格转换为word文档。
```shell
pandoc demo.md -o demo.docx
```
####文献引用
首先打开JabRef创建一个BibTex文件库，这里作为范例也可以直接打开demo文件夹中的`myref.bib`文件，通过JabRef可以对文献进行直观的管理。尝试拖动pdf到JabRef中，还能对文献的位置进行管理，便于直接通过BibTex文件文件打开需要的参考文献。
![](https://gitee.com/Astral/img/raw/master/blog/demo-preview.png)
整理好BibTex文件后便可以参考`demo-citation.md`文件对文献进行引用，引用的时候，我们使用Bibtex中每条文献信息大括号内的第一个字段，前面加上`@`符号，用方括号扩起来。需要引用多条文献的时候，在方括号内，对不同文献标记用分号区隔。此时预览中无法正确的显示引用，转换为word文档后可以正确显示和对文献进行编号。
这类文档转换为word文档时，需要指明BibTex文件和csl规范，格式如下：
```shell
pandoc --filter pandoc-citeproc --bibliography=myref.bib --csl=chinese-gb7714-2005-numeric.csl demo-citation.md -o demo-citation.docx
```
####图片编号
参考`demo-figref.md`，图片使用时，加入了一些新的信息。前面的方括号里面，加上了图标题；后面的大括号，使用#fig:id的方式，加入了图的标记。引用的时候，采用{@fig:id}的方式，分别引用每个图形。首部的4行内容用处是在文档转换将{@fig:id}中的“Figure”替换为“图”。转换命令格式为：
```shell
pandoc --filter pandoc-fignos --filter pandoc-citeproc --bibliography=myref.bib --csl=chinese-gb7714-2005-numeric.csl demo-figref.md -o demo-figref.docx
```
####补充
此文最后发布时，使用pandoc转换遇到了一些障碍，文中第一张图采用了html标签插入，使用pandoc未能成功转换，这里建议需要word版的需求的话尽可能使用纯Markdown完成。

关于如何发布到Wordpress，网上各路大神的方法很多，这里笔者直接使用了`markdown-preview-enhanced`的自带功能，直接在预览区右键，导出HTML文本，后直接粘贴在Wordpress中完成。
PS：Wordpress5以后选择HTML块粘贴即可，注意修改HTML开头的css链接，我直接将`markdown-preview-enhanced`文件夹存放在了服务器的`wp-content/styles`目录下，开头的css链接修改为了
```
<link rel="stylesheet" href="./wp-content/styles/markdown-preview-enhanced/node_modules/@shd101wyy/mume/dependencies/katex/katex.min.css">
```
![](https://gitee.com/Astral/img/raw/master/blog/截屏2020-02-10下午3.02.15.png)
代码部分我的Wordpress使用了插件`CodeColorer`，编辑`wp-content/plugins/codecolorer/codecolorer-options.php`
将130行附近的`$options['escaped']`修改为`true`；
158行附近的`$options['inline'] =false;`修改为`true`即可。
PS：vim中使用:`set nu` 可显示行号。修改完成后Wordpress的`<code>`标签默认为内联模式，而markdown解析的行内代码使用的`<code>`标签，单行代码使用的`<pre>`标签，最终显示效果接近，如本文样式。

不知什么原因，`escaped`设置为`true`后转移自负`&lt;`可以正常显示为`<`，而`'`依然显示为`&apos;`，禁用插件`CodeColorer`后恢复。为兼容以前的文章，暂时保留`CodeColorer`，下次进行站点迁移时考虑放弃使用该插件，涉及代码的文章均采用word直接发布到Wordpress或使用Markdown的形式发布。

更多用法在探索后更新
