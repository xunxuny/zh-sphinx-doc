.. highlight:: rest

.. _inline-markup:

内联标记
=============

Sphinx 使用文本解释角色在文档中插入语义标签.
这样写 ``:rolename:`content```.

.. note::

   默认角色 (```content```) 并不特别.  可使用任何其他有效的名字来代替; 使用 :confval:`default_role` 设置.

由主域添加的角色请参考 :ref:`domains` .


.. _xref-syntax:

交叉索引的语法
~~~~~~~~~~~~~~~~~~~~~~~~

多数文本解释角色都会产生交叉索引.
需要写一个 ``:role:`target```, 创建名为 *target* 的链接，类型由 *role* 指定.  链接文本与 *target* 一样.

还有其他的功能，这使得交叉索引更通用:

* 需要明确的标题及索引标签, 像reST 超链接: ``:role:`title <target>``` ，会链接 *target* 标签, 但链接文本为 *title*.

* 加前缀 ``!``, 交叉索引/超链接不会被创建.

* 前缀 ``~``, 链接文本仅是标签的最后成分.
  例如, ``:py:meth:`~Queue.Queue.get``` 会建立到 ``Queue.Queue.get`` 的链接，但是链接文本仅显示 ``get`` .

  HTML 文档, 链接的 ``title`` 属性 (显示为鼠标的tool-tip) 一直是完整的标签名.


交叉索引的对象
-------------------------

这些角色在不同主域里:

* :ref:`Python <python-roles>`
* :ref:`C <c-roles>`
* :ref:`C++ <cpp-roles>`
* :ref:`JavaScript <js-roles>`
* :ref:`ReST <rst-roles>`


.. _ref-role:

交叉索引的位置
-------------------------------------

.. rst:role:: ref

   在文档的任意位置都可以使用交叉索引, 像标准reST 标签一样使用.  
   对于文档条目这些标签名必须是唯一的.有两种方式可以链接到这些标签:

   * 标签直接放在章节标题前面, 可以通过 ``:ref:`label-name``` 引用.例如::

        .. _my-reference-label:

        Section to cross-reference
        --------------------------

        章节内容.

        需引用自身, 查看 :ref:`my-reference-label`.

     角色 ``:ref:`` 会产生这个章节的链接, 链接标题是 "Section to cross-reference".  
     章节与索引可在不同的源文件.

     自动标签也可以使用 figures: given ::

        .. _my-figure:

        .. figure:: whatever

           Figure caption

     参考 ``:ref:`my-figure``` 将在图例里插入引用索引，链接文本是 "Figure caption".

     表格也可以使用，在表格标题上使用指令 :dudir:`table` .

   * 标签不放在章节开头，需要给出明确的链接，使用语法: ``:ref:`Link title <label-name>```.

   推荐使用角色 :rst:role:`ref` 而不是标准的reStructuredText 章节链接
   (比如 ```Section title`_``) ，因为它可以在不同文件间使用，并且即使章节标题变化，所有的生成器仍支持这些索引.


参考文档
---------------------------

.. versionadded:: 0.6

可以直接链接到文档名.

.. rst:role:: doc

   链接到指定文档; 文档名可以是绝对或相对的.
   例如, 参考 ``:doc:`parrot``` 出现在文档 ``sketches/index``中, 将会链接到文档 ``sketches/parrot``.  
   如果参考是 ``:doc:`/people``` 或 ``:doc:`../people```, 将会链接到文档 ``people``.

   如果没有给出链接标题(使用: ``:doc:`Monty Python members
   </people>```), 链接标题就是文档的标题.


可下载的参考文件
------------------------------

.. versionadded:: 0.6

.. rst:role:: download

   该角色可以链接源目录里可以浏览、但不是reST格式的文档，这些文件将被下载.

   如果使用该角色，被参考的文件会自动包含到输出里(显然仅是HTML输出).
   可下载文件被放在输出目录的子目录 ``_downloads`` 里;文件名被复制.

   示例::

      查看 :download:`this example script <../example.py>`.

   文件名是当前路径的相对路径, 绝对路径则被认为以源目录为根目录的相对路径.

   文件 ``example.py`` 被复制到输出目录, 并生成链接.


其他有趣的交叉索引
-----------------------------------------

以下角色也会生成索引, 但不对应实体:

.. rst:role:: envvar

   环境变量.  会生成索引.  也会产生到指令 :rst:dir:`envvar` 的链接，如果指令存在.

.. rst:role:: token

   语法名子 (用来产生到指令 :rst:dir:`productionlist` 的链接).

.. rst:role:: keyword

   Python的关键字.  会创建这些关键字的链接.

.. rst:role:: option

   执行程序的命令行参数.  需包含连字号开头.  产生到指令 :rst:dir:`option` 的链接.


以下角色产生术语的索引:

.. rst:role:: term

   术语索引.  术语由指令 ``glossary`` 创建，包含一列术语的定义.  
   在同一文件里不能使用 ``term`` 标记,
   Python 文档有一个全局的术语文件 ``glossary.rst``.

   如果使用的术语不在术语表里, 将会产生警告.


其他语义标记
~~~~~~~~~~~~~~~~~~~~~

下面的这些角色以不同样式格式化文本:

.. rst:role:: abbr

   缩写应用.  如果角色后有个括号说明文字，在HTML时会显示成 tool-tip ,仅在LaTeX才会输出.

   例如: ``:abbr:`LIFO (last-in, first-out)```.

   .. versionadded:: 0.6

.. rst:role:: command

   系统级别的命令，例如 ``rm``.

.. rst:role:: dfn

   在文本中标记术语定义.  (不产生索引条目)

.. rst:role:: file

   文件或目录名.  可以使用花括号指示变量部分, 例如::

      ... is installed in :file:`/usr/lib/python2.{x}/site-packages` ...

   在生成文档时, ``x`` 会被Python 的次要版本号替换.

.. rst:role:: guilabel

   表示用户交互接口的标签需使用 ``guilabel`` 标记.  包含基于文本的接口如
   使用 :mod:`curses` 创建的或基于其他文本库的标签.  接口标签必须使用该角色标记，
   包括按钮，窗口标题，文件名，菜单，菜单选项，甚至选择列表里的值.

   .. versionchanged:: 1.0
      GUI 标签可以使用&标示快捷方式;
      输出时&不会显示，而是在文本下面加下划线 (例如:
      ``:guilabel:`&Cancel```).  要在输出是包含&，则使用两个&&.

.. rst:role:: kbd

   标记键值序列.  键值序列一般依赖于平台或特定应用程序的约定.  如果没有相关的约定, 
   键值序列的名字应该可以修改, 以改善新用户或非英语系使用者的体验.  例如, 一个
   *xemacs* 键序被标记为 ``:kbd:`C-x C-f```, 如果没有特定应用程序或平台可供参考，
   则同样的键序应该被标记为 ``:kbd:`Control-x Control-f```.

.. rst:role:: mailheader

   RFC 822-样式邮件头的名字.  该标记并不表明邮件头在邮件信息里使用, 而是被用来映射所有相同样式的邮件头.  
   也被用来定义有邮件头的MIME类型.  在实践中邮件头名通常以相同的方式键入, 遵循 camel-casing 约定，
   有多种通用用法时被优选采用. 例如:
   ``:mailheader:`Content-Type```.

.. rst:role:: makevar

   命令 :command:`make` 的变量名.

.. rst:role:: manpage

   参考 Unix 手册页，包含章节,例如 ``:manpage:`ls(1)```.

.. rst:role:: menuselection

   菜单选项由角色 ``menuselection`` 标记.  
   标记完整的菜单选项序列，包含子菜单和选择的特定操作，以及所有的子序列.  
   独立选项的名字使用 ``-->`` 分隔.

   例如，标记选项 "Start > Programs"::

      :menuselection:`Start --> Programs`

   选项如果包含一些指示, 例如某些操作系统会使用一些标志指示命令会打开一个对话框, 
   这些指示信息在选项名中会被忽略.

   ``menuselection`` 也支持&, 与 :rst:role:`guilabel` 一样使用.

.. rst:role:: mimetype

   MIME 类型, 或者MIME 类型的元素 (主要次要部分可以分开).

.. rst:role:: newsgroup

   Usenet 新闻组.

.. rst:role:: program

   执行程序脚本.  与某些平台的可执行文件名不同, 比如Windows 程序的 ``.exe`` (或其他)
   扩展名会被忽略.

.. rst:role:: regexp

   正则表达式，不包括引用.

.. rst:role:: samp

   一块字面量文本，如代码.  文本内可以有花括号变量，如在 :rst:role:`file` 一样.  
   例如, 在 ``:samp:`print 1+{variable}```, ``variable`` 的部分会被强调.

   如不需要变量部分，使用标准代码即可.

角色 :rst:role:`index` 会产生索引条目.

下面的角色会产生外部链接:

.. rst:role:: pep

   对Python Enhancement Proposal 的参考.  会产生适当的索引条目及文本 "PEP *number*\ " ; 
   在HTML 文档,该文本是指向在线PEP文档的超链接.  可以链接到特定章节 ``:pep:`number#anchor```.

.. rst:role:: rfc

   Internet Request for Comments的参考.  也会产生索引条目及文本 "RFC *number*\ " ; 
   在HTML文档里是一个超链接，指定链接章节 ``:rfc:`number#anchor```.


如果没有特定的角色能够包含需要的超链接，就使用标准reST 标记.


.. _default-substitutions:

替换
~~~~~~~~~~~~~

文档系统提供三种默认定义的替换，可在配置文件里设置.

.. describe:: |release|

   被项目文档的发布版本替换.  这时版本字符串包含完整的标签 alpha/beta/release ,例如 ``2.5.2b3``.  由 :confval:`release` 设置.

.. describe:: |version|

   被项目文档的版本替换. 版本字符串仅有主要和次要两部分组成，例如版本2.5.1会表示为 ``2.5``.  由 :confval:`version` 设置.

.. describe:: |today|

   替换今天的日期 (文档被读取的日期), 或者配置文件设置的日期.  默认格式为 ``April 14, 2007``.  可设置 :confval:`today_fmt` 及 :confval:`today` .
