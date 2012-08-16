.. highlight:: rest

.. _code-examples:

展示示例代码
---------------------

.. index:: pair: code; examples
           single: sourcecode

示例的Python源代码或者交互界面都可以使用标准reST模块实现.在正常段落后面跟着 ``::`` 开始，再加上适当缩进.

交互界面需包含提示及Python代码的输出.  交互界面没有特别的标记.  在最后一行输入或输出之后，不应出现空的提示; 这是一个什么都不做的例子::

   >>> 1 + 1
   2
   >>>

语法高亮显示由 `Pygments <http://pygments.org>`_ (如果安装) 优雅的显示:

* 每个源文件都有高亮语言"highlighting language".  默认是
  ``'python'`` ，多数文件会高亮显示 Python 代码段,
  可以在 :confval:`highlight_language` 配置.

* 有了Python 高亮显示模块, 交互界面会自动识别并且适当强调显示.  一般Python 代码仅在可解析时高亮显示
  (使用默认的Python, 但是零散的代码段比如shell命令等代码块将不会像Python一样高亮显示).

* 高亮显示语言也可以通过指令 ``highlight`` 改变,如下::

     .. highlight:: c

  C 语言将会被使用直到下一个 ``highlight`` 指令.

* 如果文档需展示不同语言片段, 直接使用 :rst:dir:`code-block` 指令给出高亮语言::

     .. code-block:: ruby

        Some Ruby code.

  指令别名也可用于  :rst:dir:`sourcecode` .

* 有效的语言:

  * ``none`` (没有高亮显示)
  * ``python`` (默认， :confval:`highlight_language` 没有设置时)
  * ``guess`` (让 Pygments 根据内容去决定, 仅支持一些可识别的语言)
  * ``rest``
  * ``c``
  * ... 其他Pygments 支持的语言名.

* 如果选定语言的高亮显示失败，则模块不会以其他方式高亮显示.

行号
^^^^^^^^^^^^

如果安装好, Pygments可以为代码块产生行号.自动高亮显示模块 (以 ``::`` 开始), 行号由指令 :rst:dir:`highlight` 的选项 ``linenothreshold`` 管理::

   .. highlight:: python
      :linenothreshold: 5

如果代码块多于5行将产生行号.

对于 :rst:dir:`code-block` 模块, 选项 ``linenos`` 给出则为独立块生成行号::

   .. code-block:: ruby
      :linenos:

      Some more Ruby code.

另外, 选项 ``emphasize-lines`` 可以生成特别强调的行::

    .. code-block:: python
       :emphasize-lines: 3,5

       def some_function():
           interesting = False
           print 'This line is highlighted.'
           print 'This one is not...'
           print '...but this one is.'

.. versionchanged:: 1.1
   添加了``emphasize-lines`` .


包含
^^^^^^^^

.. rst:directive:: .. literalinclude:: filename

   目录里不显示的文件可能被一个外部纯文本文件保存为例子文本.  文件使用指令 ``literalinclude`` 包含. 
   [1]_ 例如包含Python源文件 :file:`example.py`, 使用::

      .. literalinclude:: example.py

   文件名为当前文件的相对路径.  如果是绝对路径 (以 ``/`` 开始), 则是源目录的相对路径.

   输入标签可以扩展，给出 ``tab-width`` 选项指定标签宽度.

   该指令也支持 ``linenos`` 选项产生行号, ``emphasize-lines`` 选项生成强调行, 
   以及 ``language`` 选项选择不同于当前文件使用的标准语言的语言.  例如::

      .. literalinclude:: example.rb
         :language: ruby
         :emphasize-lines: 12,15-18
         :linenos:

   被包含文件的编码会被认定为 :confval:`source_encoding`.
   如果文件有不同的编码，可以使用 ``encoding`` 选项::

      .. literalinclude:: example.py
         :encoding: latin-1

   指令支持包含文件的一部分.  例如
   Python模块, 可以选择类，函数或方法，使用 ``pyobject`` 选项::

      .. literalinclude:: example.py
         :pyobject: Timer.start

   这会包含文件中 ``Timer`` 类的 ``start()`` 方法后面的代码行.

   使用 ``lines`` 选项精确的控制所包含的行::

      .. literalinclude:: example.py
         :lines: 1,3,5-10,20-

   包含1, 3, 5 到 10 及 20 之后的代码行.

   另一种实现包含文件特定部分的方式是使用 ``start-after`` 或 ``end-before`` 选项 (仅使用一种).  
   选项 ``start-after`` 给出一个字符串, 第一行包含该字符串后面的所有行均被包含.  
   选项 ``end-before`` 也是给出一个字符串，包含该字符串的第一行前面的文本将会被包含.

   可以往包含代码的首尾添加新行，使用 ``prepend`` 及 ``append`` 选项.  
   这很有用，比如在高亮显示的PHP 代码里不能包含 ``<?php``/``?>`` 标签.

   .. versionadded:: 0.4.3
      选项 ``encoding`` .
   .. versionadded:: 0.6
      选项 ``pyobject``, ``lines``, ``start-after`` 及 ``end-before`` ,
      并支持绝对文件名.
   .. versionadded:: 1.0
      选项 ``prepend`` 、 ``append`` 及 ``tab-width``.


.. rubric:: Footnotes

.. [1] 标准包含指令 ``.. include`` , 如果文件不存在会抛出异常.  这一个则仅会产生警告.
