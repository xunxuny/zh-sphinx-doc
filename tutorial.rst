.. highlight:: rst

Sphinx初尝
=======================

此文档是Sphinx使用的综览性教程，包含Sphinx常用的任务处理.

绿色箭头链接了任务操作的详细信息.

配置文档源
------------------------------------

文档集的根目录叫 :term:`source directory`.  该目录也包含了 Sphinx 的配置文件 :file:`conf.py`, 在这里你可以配置Sphinx各个方面，使Sphinx按照你的要求读取源文件并创建文档.  [#]_

Sphinx 有个脚本叫做 :program:`sphinx-quickstart` ,它可以帮你建立源目录及默认配置文件 :file:`conf.py` ，它通过几个简单的问题获取一些有用的配置值.
你仅需要运行 ::

   $ sphinx-quickstart

然后回答这些问题.  (其中"autodoc" 扩展选项请选中.)

它也会自动匹配 "API 文档" 生成器 :program:`sphinx-apidoc`; 详细信息请参考 :ref:`invocation-apidoc`.


定义文档结构
---------------------------

假定你已经运行了 :program:`sphinx-quickstart` .  它创建了源目录，包含 :file:`conf.py` 
及一份主文档 :file:`index.rst` (如果你接受了默认选项).主文档 :term:`master document` 的主要功能是被
转换成欢迎页, 它包含一个目录表（ "table of contents tree"或者 *toctree* ). Sphinx 主要功能是使用
reStructuredText, 把许多文件组织成一份结构合理的文档.

.. sidebar:: reStructuredText 导读

   ``toctree`` 是 reStructuredText的 :dfn:`directive` （指令）, 一种用途十分广泛的块标记.  定义了参数、选项及目录.

   *Arguments* 直接在双冒号后面给出指令的名字.  每个指令都有不定个数的参数.

   *Options* 在参数后以"字段列表"的形式给出.  如
   ``maxdepth`` 是 ``toctree`` 指令的选项之一.

   *Content* 具体内容,在选项或参数的后面，隔开一个空行.  每个指令后面都跟着不同作用的内容.

   共同的约定是 **内容与选项一般有相同的缩进** .


toctree 指令初始为空, 如下::

   .. toctree::
      :maxdepth: 2

你可以在 *content* 的位置添加文档列表::

   .. toctree::
      :maxdepth: 2

      intro
      tutorial
      ...

以上精确展示toctree 与文档的转换.  所有的文档以文件名 :term:`document name`\ s的形式给出, 
不需文件后缀名;使用斜线作为目录分隔符.

|more| 更多信息请查看 :ref:`the toctree directive <toctree-directive>`.

现在可以创建toctree指令后的文件及目录了，
它们的章节标题被插入到toctree指令的位置 (与 "maxdepth" 同一缩进) . 现在Sphinx已知道文档的分层结构. 
(toctree指令后的文件也可以有 ``toctree`` 指令, 会生成更深的层次结构.)


添加内容
--------------

在Sphinx源文件里, 可以使用reStructuredText的很多特性.
也有些特性被添加到Sphinx中.  例如, 可以引用参考文件链接 (对所有输出类型均有效) ，使用 :rst:role:`ref` 角色.

又如, 浏览HTML版本时想要查看文档的源文件，只需点击边框栏的"显示源代码".

|more|  :ref:`rst-primer` 详细介绍了reStructuredText  
  :ref:`sphinxmarkup` 列出了Sphinx添加的全部标记.


运行创建工具
-----------------

现在已经添加了一些文件,下面可以创建文档了.  
创建工具 :program:`sphinx-build` , 使用方式 ::

   $ sphinx-build -b html sourcedir builddir

*sourcedir* 是源目录  :term:`source directory` , *builddir* 则是放置生成的文档的根目录. :option:`-b` 是创建工具的选项;这个例子创建HTML文件.

|more|  :ref:`invocation` 列出工具 :program:`sphinx-build` 
支持的所有选项.

而且, :program:`sphinx-quickstart` 脚本创建的 :file:`Makefile` 和 
 :file:`make.bat` 使操作更容易，仅需运行 ::

   $ make html

创建 HTML 在设定好的目录里.  执行 ``make`` 将不需要任何参数.

.. admonition:: 怎样产生PDF 文档?

   ``make latexpdf`` 运行在 :mod:`LaTeX builder
   <sphinx.builders.latex.LaTeXBuilder>` ,点击可以获取pdfTeX工具链.



文档对象
-------------------

Sphinx的对象 :dfn:`objects` (一般含义）在任何 :dfn:`domain` （主域）里是指简单的文档.  一个主域包含所有的对象类型, 
完整的生成标记或引用对象的描述.
最著名的主域是Python 主域.  Python文档建立函数 ``enumerate()`` , 在源文件里添加::

   .. py:function:: enumerate(sequence[, start=0])

      返回一个迭代器，输出包含索引及*sequence*里所有条目的元组. 

返回形式为:

.. py:function:: enumerate(sequence[, start=0])

   返回一个迭代器，输出包含索引及*sequence*里所有条目的元组

指令的参数是对象的描述标示 :dfn:`signature` , 内容是对它的说明.同一行可以写多个参数.

Python 主域通常是默认的, 因此不需要特别标记出主域的名字::

   .. function:: enumerate(sequence[, start=0])

      ...

以上在默认主域配置下效果是等同的.

对不同的Python 对象有不同的指令,
如 :rst:dir:`py:class` 或者 :rst:dir:`py:method` .  不同的对象类型有不同的引用角色 :dfn:`role` .  
这个标记将创建链接到文档的 ``enumerate()`` ::

   这个 :py:func:`enumerate` 函数用于 ...

这是一个实例: 可链接 :func:`enumerate` .

同样如果默认为 Python 主域 ``py:`` 可以省略.  但这不重要，Sphinx会自动发现包含 ``enumerate()`` 的文件并且链接.

不同主域对于不同标示有特定的角色，以使输出格式更美观，在C/C++
主域里增加了链接到元素类型的角色.

|more|  :ref:`domains` 列出所有主域及其指令/角色.


基本配置
-------------------

前面提到的文件 :file:`conf.py` ，控制着Sphinx怎样生成文档. 
这个文件以Python 源文件的形式执行你的配置信息 .
高级的使用者则通过Sphinx使其执行, 可以配置它实现不平凡的任务, 例如继承 :data:`sys.path` 或者导入
模块标示文档的版本.

仅需要修改 :file:`conf.py` ,可以改变默认值, 删除一些符号，修改对应的值. 
(通过标准的 Python 操作符: ``#`` 为注释行).或者通过 :program:`sphinx-quickstart` 初始化一些值.
自定义的配置一般不会由 :program:`sphinx-quickstart` 自动产生,需要自己添加标记.
记住此文件使用Python 的操作符及字符串、数字、列表等.这个文件默认保存为UTF-8编码, 首行需要添加编码声明.  
插入非ASCII字符, 则需要使用Python Unicode 字符串 (如 ``project = u'Exposé'`` ).

|more| 详情查看  :ref:`build-config` .


自动文档
--------------------

Python 源代码的文档字符串一般放置了许多的说明信息.  Sphinx 支持自动摄取这些说明信息,
使用 "autodoc"的扩展  :dfn:`extension` (标准的Python模块扩展,为Sphinx提供的附加功能).

使用autodoc, 需在配置里激活，在  :file:`conf.py` 放入字符串 ``'sphinx.ext.autodoc'`` 
位置在 :confval:`extensions` 配置值列表.  现在已配置了一些附加指令.

如,文档化函数 ``io.open()`` ,读取源码的标示及文档字符串,这样写::

   .. autofunction:: io.open

也可以读取整个类或模块, 使用选项 ::

   .. automodule:: io
      :members:

autodoc 需要导入到你的模块以便索取文档字符串.
因此,在  :file:`conf.py` 需要为  :py:data:`sys.path` 添加合适的路径.

|more|  详情请参考 :mod:`sphinx.ext.autodoc` .

其他话题
-------------------------

- 其他扩展 (math, intersphinx, viewcode, doctest)
- 静态文件
- 选择主题
- 模板
- 使用扩展
- 写扩展


.. rubric:: 尾注

.. [#] 这只是一般情况. :file:`conf.py` 可以被移动到其他目录，请参考 :term:`configuration directory` 及 :ref:`invocation` .

.. |more| image:: more.png
          :align: middle
          :alt: more info
