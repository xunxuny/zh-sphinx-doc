.. highlight:: rest

未分类标记
====================

.. _metadata:

文件范围的元数据
------------------

reST 有字段列表"field lists" 的概念; 字段序列如下::

   :fieldname: Field content

文件开端的字段列表会被文档工具解释为文档源信息,通常记录了作者，出版日期等元数据.  
在Sphinx中, 在所有标记前面的字段列表将作为文档元数据放在Sphinx 环境中,不显示在输出文档中; 
在文档标题后的字段列表仍然是文档源信息的一部分显示在输出文档中.

此时, 这些元数据字段会被识别:

``tocdepth``
   文件目录表的最大深度.

   .. versionadded:: 0.4

``nocomments``
   如果设置了, 网页不会显示源文件生成的评论.

``orphan``
   如果设置, 不在目录结构中的文件产生的警告会被忽略.

   .. versionadded:: 1.0


元信息标记
-----------------------

.. rst:directive:: .. sectionauthor:: name <email>

   当前章节作者标示.  参数是作者名字,可以展示或放在邮件地址中. 地址的主域名通常要小写.
   例如::

      .. sectionauthor:: Guido van Rossum <guido@python.org>

   默认这些标记不会出现在输出文档中 (对追述贡献有帮助), 可以设置 :confval:`show_authors` 的值为真，使其产生一段输出.


.. rst:directive:: .. codeauthor:: name <email>

   指令 :rst:dir:`codeauthor` , 可多次出现，记录代码的作者，
   就像 :rst:dir:`sectionauthor` 记录文档章节的作者一样.  
   在 :confval:`show_authors` 为真时才显示在输出中.


索引生成标记
-----------------------

Sphinx 自动从对象(函数、类及属性)说明中生成索引条目;在 :ref:`domains` 也有讨论.

这是个明确的标记,使得生成的索引更全面, 索引条目将会包含信息单元的次要信息，如语言参考.

.. rst:directive:: .. index:: <entries>

   指令包含一到多条索引条目.  每个条目有类型和值组成，以冒号分隔.

   例如::

      .. index::
         single: execution; context
         module: __main__
         module: sys
         triple: module; search; path

      The execution context
      ---------------------

      ...

   这个指令包含5个条目, 产生的索引会链接到页面确切的位置(离线时是相关的页码).

   索引指令会在源位置插入参考标签, 并会放在它们实际所映射内容的前面，上面例子中实际映射内容是标题.

   条目类型:

   single
      创建单一索引条目.  可以使用分号分隔子条目(该符号也用来描述创建了那些条目).
   pair
      ``pair: loop; statement`` 创建两个索引条目的简写,
      命名为 ``loop; statement`` 或 ``statement; loop``.
   triple
      例如 ``triple: module; search; path`` 创建三个条目的简写, 它们是 ``module; search path``, ``search; path,
      module`` 及 ``path; module search``.
   see
      ``see: entry; other`` 创建可以映射到其他条目的索引.
   seealso
      如 ``see``, 但是插入 "see also" 代替 "see".
   模块, 关键字, 操作符, 对象, 异常, 声明, 内建指令均会创建两个索引条目.  
      例如, ``module: hashlib``会创建条目 ``module; hashlib`` 和 ``hashlib; module``.  
      (这是Python特定的，因此不推荐使用)

   可以加前缀感叹号表示主要的索引条目.  主要索引会被强调显示.  例如, 有两个文件包含 ::

      .. index:: Python

   一个文件包含 ::

      .. index:: ! Python

   在反向链接中后面那个的索引会被强调.

   索引指令仅包含单一条目，这是简短的用法::

      .. index:: BNF, grammar, syntax, notation

   创建了4个条目.

   .. versionchanged:: 1.1
      添加了 ``see`` and ``seealso`` 类型, 及主条目标记.

.. rst:role:: index

   当指令 :rst:dir:`index` 在模块级别并链接到下一段的开头, 仍有相应的角色在使用的地方设置链接标签.

   角色的内容可以是一个短语,保留在文本中并作为索引条目使用.  
   也可以是文本与索引条目的组合，看起来是明确的参考文献标记.  
   这时, 标记部分如指令条目的描述一样.  例如::

      一般的 reST :index:`paragraph` 包含几条 
      :index:`index entries <pair: index; entry>`.

   .. versionadded:: 1.1


.. _tags:

包含基于标签的内容
-------------------------------

.. rst:directive:: .. only:: <expression>

   当 *expression* 为真时包含指令的内容.  表达式由标签组成, 如下::

      .. only:: html and draft

   未定义的标签为假, 定义的为真 (使用 ``-t`` 命令行参数或者在文件 :file:`conf.py` 中定义) .  
   布尔表达式, 可使用括号 (如 ``html and (latex or draft)``) .

   当前生成器的格式(``html``, ``latex`` or ``text``)会被设置为标签.

   .. versionadded:: 0.6


Tables
------

使用 :ref:`standard reStructuredText tables <rst-tables>`.  在HTML中工作良好, 
但是输出LaTeX文档时经常会有些问题: 列的宽度经常不能自动正确的显示.  
因此, 出现如下指令:

.. rst:directive:: .. tabularcolumns:: column spec

   指令给出了下面文件中表格的列规格.
   这个规格是LaTeX 的 ``tabulary`` 封装环境的第二个参数( ``tabulary`` 用来翻译表格).
   如下 ::

      |l|l|l|

   这表示左调整，无分行的列.  如果列包含长文本将会自动被截断, 
   使用标准构建 ``p{width}`` , 或由 tabulary自动定义:
 
   =====    ================ 
   ``L``      左调整，自动宽度
   ``R``      右调整，自动宽度  
   ``C``      居中，自动宽度   
   ``J``      自调整，自动宽度   
   =====    ================  


   根据表格里的内容自动调节宽度, 测量标准为它们占据的总宽度.

   默认, Sphinx 使用的列布局是 ``L`` .

   .. versionadded:: 0.3

.. warning::

   表格包含列表类元素比如对象描述,模块引用等，这些列表不能在 ``tabulary`` 以外设置.  
   因此需要设置标准 LaTeX ``tabular`` 环境，或者给出 ``tabularcolumns`` 指令.  
   然后 ``tabulary`` 设置表格, 且必须使用 ``p{width}`` 构建包含这些元素的列.

   字面模块不能使用 ``tabulary`` , 包含字面模块的表格需使用 ``tabular``.  
   当然字面模块使用的字体环境仅支持 ``p{width}`` 列, 这也是默认的方式, Sphinx会生成这些表格的列规格.
   使用 :rst:dir:`tabularcolumns` 指令可以更好的控制表格.
