origin -> http://shell909090.com/blog/2012/11/python入门指引/

now/check:18.719 -> http://blog.shell909090.org/blog/archives/2272/index.html

https://github.com/shell909090/shell909090.github.io/blob/4ba1274a1d3c4f30ccda7a4469d9901dcf83865d/blog/archives/2272/index.html

else: https://github.com/shell909090/learn-python/issues/2

> PS：笨办法学python不推荐，水分大，太浪费时间

# python入门指引 

Nov 19, 2012

## 前言

其实我也不知道python怎么入门，由我来写这个真的不是很合适。我学python是直接找了dive into python来看。然后照着写了几个例子。大概两天后，就能磕磕绊绊的上路了。就好像拿筷子，都不记得怎么学会的拿筷子，怎么来教人呢？

不过最近在python-cn的列表里面，我大概连续数周都持续看到“python入门看哪本教程比较好”，实在是不堪其扰。干脆就写个简单的guide，有心的人自己看。没心的——那我也没办法了。

## 基本知识

首先，你要了解一个事情。很多你不会的东西并不属于python。例如你不知道网络通讯的流程，你不知道文件的权限和打开标志用法，你不知道fork和stdin/stdout的关系。这些python教不会你。如果你缺乏这些和语言/库无关的相关知识，请自行补课。如果你缺乏计算机基础理论，请自行补课。

因此不要随便给我发邮件/留言/咨询，为什么这个问题在python里无法解决。为什么python无法所见即所得，为什么python无法热部署，为什么python无法用于嵌入式开发。在问这个问题之前，请先确认“这是一个python的问题”。例如GIL，或者脑残lambda。如果你不确定，请自己搜索一下相关的文章，确认一下。在提问前，看看“提问的智慧”。如果你确实搜过了，找不到，那就问吧，没办法。

## 入门

在网络上，python入门的两大基础书籍分别是(后面有朋友补充了一本，我也加上)：
 - [A Byte of Python](http://www.swaroopch.com/notes/python/) [中文版](http://woodpecker.org.cn/abyteofpython_cn/chinese/)
 - [Dive Into Python](http://www.diveintopython.net/) [中文版](http://woodpecker.org.cn/diveintopython/)
 - Learn Python The Hard Way, 2nd Edition 中文版
 
后面基本就是看python-doc，我推荐你跳过一堆有的没的，直接看Library
Reference。python本身就是易读性极强的代码，文档又相当漂亮，内置库又全。大部分情况下，python-doc都应当能解决你的问题。

## web

web是程序员的一大去向。python程序员入门必须要过的一个框架就是django。不要纠结了，django在python社区中名气太大，用的人太多。因此入门材料是最多的，社区最大，门槛最低。如果你要入门web，必然从django开始。在不熟悉python的情况下，我不推荐你贸然从其他框架开始入门。
当然，如果你已经熟悉python了，考虑入门web框架，可以参考专精一节。

## 爬虫

python下说到爬虫开发，入门首选Scrapy。原因和上面一样，社区最大，用的人最多。好不好用就见仁见智了。反正我的所有爬虫框架都是用自己基于gevent写的库。

## ui
python的ui框架也很多，很复杂。同样，如果是入门，我建议从qt的两个框架，pyqt和pyside开始入门。关于这两家的恩怨我就不多废话了。

##专精

所谓专精，是指使用python在特定工作上。我们基本分为几个领域。

## 系统和部署

virtualenv：基本凡是在商用环境中部署的，建议都用这个。可以将python自带在源码里面，避免迁移/集成问题。
python-daemon：写daemon的时候比较方便。

## 网络

说到网络，基本就是除web外。
- twisted：非常强大的网络库，各种协议支持全面，不过reactor模式真是纠结。
- gevent：异步协程模式的网络库。
- Scapy：强大的网络库，基本啥都能干。
- pyzmq：我一直不觉得zeromq是一个mq。我觉得他是一个抽象网络层。

## web容器

python web框架的一大特点，是容器/框架/ORM/template可以分开自己玩。
注意，容器和框架是两码事情。容器是python web运行的环境，框架是解析环境的玩意。两者间一般都使用[wsgi接口](http://www.python.org/dev/peps/pep-0333)进行连接。这是python的标准做法，fastcgi/scgi也会被转换为wsgi进行连接。但是也不是没有其他选择。一般我们有以下模式：
- cgi：python-doc中自带了cgi模块。
- mod_python：embed in apache。

下面是wsgi接口的容器。wsgi的优点在于我们可以在这些容器上运行任意一款支持wsgi的框架。
- flup：支持提供fastcgi, scgi, AJP接口，web server可以用这三种协议进行连接。
- Google App Engine：PaaS服务。
- Gunicorn：直接提供http服务。
- mod_wsgi：使用内部协议和apache集成。
- twisted：直接提供http服务。
- tornado：直接提供http服务。
- uWSGI：使用内部协议和nginx集成。
- werkzeug：直接提供http服务。

建议的部署模式是，用apache的，去mode_wsgi。用nginx的，去uwsgi。用GAE的，直接可用。其他，通通转发。

## web
你可以参考飞龙的[这篇文章](http://feilong.me/2011/01/talk-about-python-web-framework)，里面介绍了数种框架。你可以通通玩一下，反正也不麻烦，然后选择一种最适合自己的玩意。
python中有一种不得不提的玩意就是Zope。这个东西我不知道该如何评价，有兴趣的自己看吧。

## ORM

ORM：python的ORM系统比较单一，一般都是sqlalchemy。这个框架非常强大，但是很消耗资源。有兴趣的可以去[官网](http://www.sqlalchemy.org/)上自己了解。偶尔也见用SQLObject的，不多。
ORM的另一大选择是ZODB，不过用的比较少。希望了解的自己去咨询老潘。

## template

python wiki上[有篇文章](http://wiki.python.org/moin/Templating)提到了python template engine的分类和列表。作为专精，我建议你至少玩一下string.Template，webhelpers，mako，jinja2，Genshi这几个玩意。

## 爬虫

关于python爬虫的进阶，就比较不好说。我正在写一篇长篇blog，介绍python爬虫的种种。不过至少来说，你需要了解以下几个东西：celery，beautifulsoap，lxml，selenium，phantomjs，pyquery。

## ui

gui库的列表可以看[这里](http://wiki.python.org/moin/GuiProgramming)，其中我推荐你看一下玩玩的有：PyGtk，TkInter，WxPython，Glade，pygame。

## 科学计算

不用废话，你可以看这篇文档[用Python做科学计算](http://hyry.dip.jp:8000/pydoc/index.html)。作者出书了，你可以支持一下。

## 图形处理

那必然要提到的就是pil，python imaging library。另一样要介绍的是pydot，pygraph或者pygraphviz。这不是图形库，准确的说，应当是图论库。他可以使用graphviz将图论结构转换为图像。

## 文档

- pygments：格式化代码的库，可以将文本代码格式化为不同格式的，带颜色的代码。
- markdown：格式化markdown文档为html的库。不过我觉得实现的和标准不一致，没用。
- reStructured：docutils工具组，可以转换为多种格式。
- sphinx：同样是rst的工具，可以生成多种格式。

## 进阶

首先，你应当去看沈游侠在某次cpug聚会上的讲话[Python编程艺术](http://www.slideshare.net/wilhelmshen/py-art)，这是python程序员进阶的必读。不过很可惜，slide是高桥流的，本身不是为了让你看内容而出的。而当时的演讲又没有录像（如果有的话，请给我一份拷贝，我会问沈游侠能不能放出，找空间，搞定相关问题，感谢），因此理解上相当困难。不过这里的每一句话都相当有道理，是数十年程序经验的总结。
另外，作为进阶，你可以适当的看python3的一些内容。[Dive Into Python3中文版](http://getpython3.com/diveintopython3/)。还有[pypy](http://pypy.org/)和[cython](http://cython.org/)。
作为python进阶人士，你一定要在手头备一份常用发行的[源码](http://www.python.org/download/)，不要求小版本一致，至少大版本一致（2.7.x，最后一位可以不对齐）。适当的阅读源码，尤其是Objects目录。经常重新阅读python-doc。

> Posted by Shell Xu Nov 19, 2012  Tags: [program](http://blog.shell909090.org/tags/program/) [python](http://blog.shell909090.org/tags/python/) 
