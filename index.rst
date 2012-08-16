

.. sphinx使用手册 的主入口文件, 创建于 星期五, 2 三月 2012 09:50:37 +0800.
   你可以按照自己的喜好修改该文件.

译者前言
========

sphinx使用手册,源文档地址 `Sphinx <http://sphinx.pocoo.org/>`_ .

    **用户评价:**
    ``值得欢呼的好工具，确实方便那些需要书写文档的程序员们!``

欢迎
=============

   Sphinx 是一种文档工具，它可以令人轻松的撰写出清晰且优美的文档, 由 Georg Brandl 在BSD 许可证下开发.
   `新版的Python文档 <http://docs.python.org/>`_ 就是由Sphinx生成的，
   并且它已成为Python项目首选的文档工具,同时它对 C/C++ 项目也有很好的支持; 并计划对其它开发语言添加特殊支持. 
   本站当然也是使用 Sphinx 生成的，它采用reStructuredText!
   Sphinx还在继续开发. 下面列出了其良好特性,这些特性在Python官方文档中均有体现:

    * *丰富的输出格式:* 支持 HTML (包括 Windows 帮助文档), LaTeX (可以打印PDF版本), manual pages（man 文档）, 纯文本
    * *完备的交叉引用:* 语义化的标签,并可以自动化链接函数,类,引文,术语及相似的片段信息
    * *明晰的分层结构:* 可以轻松的定义文档树,并自动化链接同级/父级/下级文章
    * *美观的自动索引:* 可自动生成美观的模块索引
    * *精确的语法高亮:* 基于 `Pygments <http://pygments.org/>`_ 自动生成语法高亮
    * *开放的扩展:* 支持代码块的自动测试,并包含Python模块的自述文档(API docs)等

   Sphinx 使用 `reStructuredText <http://docutils.sf.net/rst.html>`_ 
   作为标记语言, 可以享有 `Docutils <http://docutils.sf.net/>`_ 为reStructuredText提供的分析，转换等多种工具.
