.. highlight:: rest

段落级别的标记
----------------------

.. index:: note, warning
           pair: changes; in version

这个指令可以创建简单的段落，也可以如普通文本一样使用内部信息单位:

.. rst:directive:: .. note::

   显示用户使用API时的注意事项.  指令的内容应该使用完整的语句及标点符号.

   例如::

      .. note::

         该功能不适于发送垃圾邮件.

.. rst:directive:: .. warning::

   显示用户使用API时的注意事项.  指令包含完整的句子和标点符号. 
   不同于 :rst:dir:`note` ，它一般显示的是信息安全方面的注意事项.

.. rst:directive:: .. versionadded:: version

   标示某个版本或C语言的API 新增的特性. 应用在模块条目时，会放置在章节内容的前面.

   第一个参数必须给出版本号，可以添加第二个参数组成一个简单的说明.

   例如::

      .. versionadded:: 2.5
         The *spam* parameter.

   注意在指令头和说明中间不能有空行; 这样会使标记语言认为这个模块不是连续的.

.. rst:directive:: .. versionchanged:: version

   与 :rst:dir:`versionadded` 相似, 但它描述的是该功能在版本中的更改(新参数,效果改变等).

.. rst:directive:: .. deprecated:: version

   与 :rst:dir:`versionchanged` 相似, 描述的是功能的取消.  解释仍可以给出，比如功能的替代方案.  如::

      .. deprecated:: 3.1
         Use :func:`spam` instead.


--------------

.. rst:directive:: seealso

   许多章节包含模块文档或者扩展文档的参考索引列表.这些列表由指令 :rst:dir:`seealso` 创建.

   指令 :rst:dir:`seealso` 通常放在所有子章节的前面.对于HTML文档, 需与主文本分开.

   指令 :rst:dir:`seealso` 内容是reST的定义列表.
   例如::

      .. seealso::

         Module :py:mod:`zipfile`
            标准模块 :py:mod:`zipfile` 的文档.

         `GNU tar manual, Basic Tar Format <http://link>`_
            归档文件的文档, 包含 GNU tar 扩展.

   一个简单的形式::

      .. seealso:: modules :py:mod:`zipfile`, :py:mod:`tarfile`

   .. versionadded:: 0.5
      简单形式.

.. rst:directive:: .. rubric:: title

   该指令用来创建文档标题,但是该标题不出现在文档的目录结构中.

   .. note::

      如果标题被"Footnotes"标记出来 (或被其他语言选中), 这个标题在LaTeX会被忽略, 或假定它包含尾注定义,仅创建一个空标题 .


.. rst:directive:: centered

   该指令创建居中加粗文本行.  例如::

      .. centered:: LICENSE AGREEMENT

   .. deprecated:: 1.1
      该指令仅在旧版本里声明了.  使用 :rst:dir:`rst-class` 代替并添加适当的样式.


.. rst:directive:: hlist

   该指令生成水平列表.  它将列表项横向显示并减少项目的间距使其较为紧凑.

   生成器需支持水平分布, 这里的 ``columns`` 选项定义显示的列数，默认为2.  例如::

      .. hlist::
         :columns: 3

         * 列表
         * 的子
         * 项会
         * 水平
         * 排列

   .. versionadded:: 0.6


目录表格标记
------------------------

指令 :rst:dir:`toctree` ，会产生子文档的目录表格, 详见 :ref:`toctree-directive`.

本地目录表, 则使用标准 reST :dudir:`contents directive
<table-of-contents>`.


术语
--------

.. rst:directive:: .. glossary::

   该指令必然包含一个reST式的定义列表标记，由术语和定义组成.  这些定义其后可被 :rst:role:`term` 引用.  例如::

      .. glossary::

         environment
            一个结构，包含信息是所有文档的保存路径，使用的参考文献等.  
            在解析的阶段使用，因此连续运行时仅需解析新的或修改过的文档.

         source directory
            根路径，包含子目录，包含一个Sphinx工程的所有源文件.

   与标准的定义列表相比, 支持多个术语且这些术语可以有内联标记.  可以链接所有术语.  例如::

      .. glossary::

         term 1
         term 2
            定义两个术语.

   (术语排序时，通过第一个术语决定顺序.)

   .. versionadded:: 0.6
      给出术语指令的 ``:sorted:`` 选项，则术语就会按照字母自动排序.

   .. versionchanged:: 1.1
      开始支持多术语和术语的内联标记.


语法产品的显示
---------------------------

特殊标记形成了一套语法展示产品.
这些标记很简单，不会试图模型化BNF的各个方面(及其派生形式), 但是提供了足够显示上下文的语法信息，定义符号将以超链接符形式显示.  指令如下:

.. rst:directive:: .. productionlist:: [name]

   该指令后跟一组产品.  每个产品一行，有名字组成，与后面的定义通过冒号分隔.  
   如果定义有多行，后面的行以冒号开始，且冒号垂直对齐.

   :rst:dir:`productionlist` 的参数用来区分不同语法产品的列表.

   在 ``productionlist`` 指令参数间不允许有空行.

   定义可以包含别名，以解释文本给出(例如 ``sum ::= `integer` "+" `integer```) -- 这会生成产品别名的参照表.  
   除了产品列表，还可以使用别名访问 :rst:role:`token`.

   注意产品内部没有完整的reST解释器, 因此不能避免使用 ``*`` 或 ``|`` 字符.

下面是Python 参考手册的例子::

   .. productionlist::
      try_stmt: try1_stmt | try2_stmt
      try1_stmt: "try" ":" `suite`
               : ("except" [`expression` ["," `target`]] ":" `suite`)+
               : ["else" ":" `suite`]
               : ["finally" ":" `suite`]
      try2_stmt: "try" ":" `suite`
               : "finally" ":" `suite`
