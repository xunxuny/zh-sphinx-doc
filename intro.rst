引言
============

该文档是Sphinx建立文档的参考.  Sphinx 将 reStructuredText_  源文件集转换为丰富的输出格式，并自动产生参考文献、索引等.
简言之，如果你有一个包含reST-格式的文档的目录（包含文档的所有文件或子目录）, 
Sphinx 会生成组织合理的HTML文件（在另一个目录里），使得浏览及导航功能使用非常方便.  
通用一份源文件，你可以生成LaTeX 文件，然后编译成 PDF 版本的文档,
也可以直接使用 `rst2pdf <http://rst2pdf.googlecode.com>`_ 生成PDF 文件.

重点讨论的是手写文档而不是自动生成的API文档.
但是我们对于两种都支持的很好，甚至支持两种内容混合的文档, 
假如你需要纯净的API文档，查看 `Epydoc <http://epydoc.sf.net/>`_, 它可以解析 reST.


不同文档系统的转换
-----------------------------

这一节搜集了一些有用的提示，帮助我们从其他的文档系统迁移到reStructuredText/Sphinx.

* Gerard Flanagan （人名）写了一个脚本把纯净的HTML转换为 reST文本; 
  你可以到 `Python 索引页 <http://pypi.python.org/pypi/html2rest>`_ 查看.

* 原来的Python文档转换为 Sphinx, 
  代码托管在 `the Python SVN repository
  <http://svn.python.org/projects/doctools/converter>`_.  
  它包含将Python-doc-style LaTeX 标记转换为Sphinx reST 的生成代码.

* Marcin Wojdyr 写了一个脚本，将 Docbook 转换为 reST ; 可查看 `Google Code <http://code.google.com/p/db2rst/>`_.

* Christophe de Vienne 写了一个将 Open/LibreOffice 文档转换为
  Sphinx的工具: `odt2sphinx <http://pypi.python.org/pypi/odt2sphinx/>`_.

* 转换不同的标记语言, `Pandoc <http://johnmacfarlane.net/pandoc/>`_ 也是一个非常有用的工具.


在其他系统中使用
----------------------

请参考 :ref:`pertinent section in the FAQ list <usingwith>`.


前提
-------------

Sphinx 运行前需要安装 **Python 2.4** 或者 **Python 3.1** , 以及
docutils_ 和 Jinja2_ 库.  Sphinx 必须工作在 0.7 版本及一些 SVN 快照(不能损坏).  
如果需要源码支持高亮显示，则必须安装 Pygments_ 库.

如果使用 **Python 2.4** ，还需要 uuid_.

.. _reStructuredText: http://docutils.sf.net/rst.html
.. _docutils: http://docutils.sf.net/
.. _Jinja2: http://jinja.pocoo.org/
.. _Pygments: http://pygments.org/
.. The given homepage is only a directory listing so I'm using the pypi site.
.. _uuid: http://pypi.python.org/pypi/uuid/


用法
-----

更深入的话题,请参考 :doc:`tutorial` . 
