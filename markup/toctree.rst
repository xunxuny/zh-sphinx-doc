.. highlight:: rst
.. _toctree-directive:

目录树
============

.. index:: pair: table of; contents

目前 reST 还没有专门的语法表示文件的相互关联或怎样将一份文档拆分成多个输出文件， 
Sphinx 使用自定义的指令在独立文件里添加这种关系或目录表格.  
指令 ``toctree`` 是其核心元素.

.. note::

   简单的在一个文件里包含另一个文件也可以完成包含指令 :dudir:`include` .

.. rst:directive:: toctree

   该指令在当前位置插入一个目录树 "TOC tree" ,在文档中使用独立的 TOCs (包括 "sub-TOC trees")给出指令的主体.  
   相对文件名 (不以缩写开头) 是指令所在的文件的相对路径，绝对文件名则以源目录为根目录.  
   数值 ``maxdepth`` 选项指定目录的层次，默认包含所有的层次. [#]_

   下面是一个例子 (以Python文档库作为参考)::

      .. toctree::
         :maxdepth: 2

         intro
         strings
         datatypes
         numeric
         (更多的文档列在下面)

   它实现了两种功能:

   * 插入所有文档的目录表格，深度为2表示文档必须有一个标题.
     这些文档内的指令 ``toctree`` 也会被插入.
   * Sphinx 确定了 ``intro``, ``strings`` 这几个字符串在文档中的相对顺序，并知道它们是本文档的子页面，是文档库的索引.  
     根据这些信息可产生 "下一个主题", "上一个主题" 及 "父页面" 的链接.

   **条目**

   目录树里的标题是由 :rst:dir:`toctree` 指令自动罗列其包含文档的标题. 如果不合适，
   可以使用与reST超链接相似的标签符号自定义一个标题，(或使用Sphinx的 :ref:`cross-referencing syntax <xref-syntax>`). 
   如下::

       .. toctree::

          intro
          All about strings <strings>
          datatypes

   上面的第二行中 ``strings`` 是文档名, 但是在目录树里会使用 "All about strings" 作为标题名.

   也可以添加外部链接，只要使用HTTP URL 代替文档名就可以了.

   **章节编号**

   如果希望在HTML为章节编号，仅需给出选项 ``numbered`` .  例如::

      .. toctree::
         :numbered:

         foo
         bar

   编号以标题 ``foo`` 开始.子目录也会自动编号 (不需在给出 ``numbered`` 选项).

   也可以定义编号的深度, 需在 ``numbered`` 后给出深度的参数.

   **其他选项**

   如果希望目录里仅出现文档的标题，不出现文中其他同等级的标题行（同一缩进）, 可以使用选项 ``titlesonly`` ::

      .. toctree::
         :titlesonly:

         foo
         bar

   使用匹配指令 "globbing" , 只需给出 ``glob`` 选项.  可用文档列表里的所有条目都会被匹配，
   并且按照字母顺序插入 .  例如::

      .. toctree::
         :glob:

         intro*
         recipe/*
         *

   以上会包含所有以 ``intro`` 开头的文档及 ``recipe`` 目录下的所有文件,第三行匹配所有剩下的文件 (除了包含该目录树指令的文件,即当前文件.) [#]_

   特殊名字 ``self`` 可以代替当前文件.  这在从目录树生成导航地图（ "sitemap" ）时非常有用.

   还可以给出 "hidden" 选项, 如下::

      .. toctree::
         :hidden:

         doc_1
         doc_2

   文件仍会存在于Sphinx 的文档结构中，但是不会在当前指令位置插入目录 -- 其后可以按照特定的方式插入该文件的链接，比如在HTML边框栏里.

   最后, 在 :term:`source directory` (包括子目录)里的所有文件都需出现在某个 ``toctree`` 指令里;
   否则Sphinx会报出警告, 因为该文件没有通过标准导航.
   可以使用 :confval:`unused_docs` 排除某些文件，使用 :confval:`exclude_trees` 排除整个目录.

   主文档（ "master document" ）(由 :confval:`master_doc` 指定) 是整个目录结构的根.  
   可以作为文档的主页面, 如果不给出 ``maxdepth`` 选项，则会是"填满目录内容的表格".

   .. versionchanged:: 0.3
      增加 "globbing" 选项.

   .. versionchanged:: 0.6
      增加 "numbered" 及 "hidden" 选项，及外部链接，支持"self" 关键字.

   .. versionchanged:: 1.0
      增加 "titlesonly" 选项.

   .. versionchanged:: 1.1
      增加"numbered"选项的数值参数 .


预留名子
-------------

Sphinx 有些保留的文档名; 试图创建这些名字的文档会产生错误.

这些特殊的文档名 (生成的页面) 有:

* ``genindex``, ``modindex``, ``search``

  分别对应通用索引, Python模块索引, 及搜索页面 .

  通用索引封装了模块条目，所有
  :ref:`object descriptions <basic-domain-markup>` 生成的索引, 及 :rst:dir:`index`
  指令生成的索引.

  Python模块索引包含每个 :rst:dir:`py:module` 指令生成的索引.

  搜索页面包含的表单使用JSON格式的搜索索引，然后JavaScript根据输入的搜索词,
  全文搜索整个文档;因此,需要工作在支持现代JavaScript的浏览器中.

* 名字以 ``_`` 开头

  尽管仅有少数预留的文档名还被使用, 但是最好不要创建同名文档或在文档路径中包含这些名字.
  (使用 ``_`` 前缀定义模板路径是个好方法.)


.. rubric:: Footnotes

.. [#] 选项 ``maxdepth`` 不适用于 LaTeX , 其在文档开始部分就会出现包含所有文件的目录表, 
       它的深度使用 ``tocdepth`` 计数器控制, 可以使用 :confval:`latex_preamble` 重新配置，例如 ``\setcounter{tocdepth}{2}``.

.. [#] 所有可以使用的匹配符号: 标准 shell 表达式如 ``*``, ``?``, ``[...]`` 及 ``[!...]`` ，但其不匹配斜杠.  
       使用双星号 ``**`` 可以匹配任何包含斜杠的字符串.
