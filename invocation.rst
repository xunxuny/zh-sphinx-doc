.. _invocation:

调用 sphinx-build
==========================

脚本 :program:`sphinx-build` 用来建立Sphinx文档集.
调用方式::

     $ sphinx-build [options] sourcedir builddir [filenames]

*sourcedir* 是源文件目录  :term:`source directory` , *builddir* 是生成文件目录.一般不需要写 *filenames* .

脚本 :program:`sphinx-build` 的选项:

.. program:: sphinx-build

.. option:: -b 生成器名字

   生成器,决定了生成文档的类型,是最重要的选项.  通用的生成器有:

   **html**
      生成HTML文档.  默认的生成器.

   **dirhtml**
      生成HTML文档，但是每个文档都有单一的目录，在用浏览器访问时有漂亮的URLs (没有后缀 ``.html`` ) .

   **singlehtml**
      所有内容生成单一的 HTML .

   **htmlhelp**, **qthelp**, **devhelp**, **epub**
      生成HTML文档，建立文档集时包含这些类型之一的额外信息.

   **latex**
      生成 LaTeX 源，可使用 :program:`pdflatex` 将其编译成 PDF 文档.

   **man**
      生成UNIX系统的groff格式手册.

   **texinfo**
      生成 Texinfo 文件，可以使用 :program:`makeinfo` 产生Info 文件.

   **text**
      生成纯文本文件.

   **gettext**
      生成 gettext-style 分类信息  ( ``.pot`` 文件).

   **doctest**
      运行文档集内所有测试，如果 :mod:`~sphinx.ext.doctest` 扩展可用.

   **linkcheck**
      检查所有外部链接的可信度.

   查看 :ref:`builders` ，列出了Sphinx支持的所有生成器及
   其可添加的扩展.

.. option:: -a

   给出时重写全部文档，默认则仅重新生成有新的源文件或源文件被修改的文档.(不适用于所有生成器.)

.. option:: -E

   不使用保存的 :term:`environment` (环境，缓存了所有的参考索引), 而是完全重建.  
   默认仅读取和解析最近新添加及改动的源文件.

.. option:: -t tag

   定义标签 *tag*.  与 :rst:dir:`only` 指令相关，标签是一个目录集合，仅处理标签目录中的内容.

   .. versionadded:: 0.6

.. option:: -d 路径

   目前Sphinx生成输出前会读取和解析所有的源文件, 
   解析过的源文件被缓存成 "doctree pickles".
   通常，这些文件被放在生成目录的 :file:`.doctrees` 文件夹中; 
   这个选项可以选择不同的缓存目录( doctrees 可以被所有的生存器共享).

.. option:: -c 路径

   不使用源目录下的 :file:`conf.py` 而是使用指定的配置文件.  
   注意在配置文件中提及的路径都是相对配置文件所在目录的相对路径,因此路径必须一致.

   .. versionadded:: 0.3

.. option:: -C

   不查找配置文件，仅使用选项 ``-D`` 的配置.

   .. versionadded:: 0.5

.. option:: -D setting=value

   覆盖 :file:`conf.py` 里的配置值.  value 是一个字符串或字典. 
   例如: ``-D latex_elements.docclass=scrartcl``.  
   布尔值使用 ``0`` 或 ``1`` 代替.

   .. versionchanged:: 0.6
      值可以为一个字典.

.. option:: -A name=value

   模板里的 *name* 变量使用 *value* 值代替.

   .. versionadded:: 0.5

.. option:: -n

   采用 nit-picky 模式.  该模式下所有错误都会产生警告信息.

.. option:: -N

   不产生彩色输出.  (在 Windows, 彩色输出一直是不可用的.)

.. option:: -q

   不产生标准输出，仅使用标准错误输出输出警告和错误信息.

.. option:: -Q

   不产生标准输出，也不产生警告信息，仅使用标准错误输出输出错误信息.

.. option:: -w file

   除标准错误输出外，将警告（错误）输出到指定文件.

.. option:: -W

   将警告视为错误.产生第一个警告就停止文档生成活动， ``sphinx-build`` 在状态1 退出.

.. option:: -P

   发生未绑定的异常时运行Python 调试器 :mod:`pdb`.(仅在调试时使用.) 


源目录与目标目录后面，可以给出一个到多个文件名.  Sphinx会尝试仅生成这些文件(及其依赖文件).


Makefile 选项
----------------

文件 :file:`Makefile` 及 :file:`make.bat` 由
:program:`sphinx-quickstart` 创建，脚本 :program:`sphinx-build` 仅使用选项
:option:`-b` 和 :option:`-d` .它们则支持以下自定义行为的变量:

.. describe:: PAPER

   :confval:`latex_paper_size` 的值.

.. describe:: SPHINXBUILD

   命令 ``sphinx-build`` 替代值.

.. describe:: BUILDDIR

   替代运行 :program:`sphinx-quickstart` 选择的目标目录.

.. describe:: SPHINXOPTS

   :program:`sphinx-build` 的额外选项.


.. _invocation-apidoc:

调用 sphinx-apidoc
===========================

程序 :program:`sphinx-apidoc` 将Python页面自动生成API文档.调用方式::

     $ sphinx-apidoc [options] -o outputdir packagedir [pathnames]

这里 *packagedir* 是生成文档的页面的根目录， *outputdir* 则是生成源文件的输出目录.
*pathnames* 给出的路径在生成时不会被忽略.


脚本 :program:`sphinx-apidoc` 也有一些选项:

.. program:: sphinx-apidoc

.. option:: -o outputdir

   给出文档页的根目录.

.. option:: -f, --force

   通常sphinx-apidoc 不会重写任何文件.  使用该项强制重写所有文件.

.. option:: -n, --dry-run

   采用该选项，将不会产生任何文件.

.. option:: -s suffix

   生成文件的后缀名，默认为 ``rst``.

.. option:: -d maxdepth

   目录的最大层次.

.. option:: -T, --no-toc

   避免生成文件 ``modules.rst``.
   当有选项 :option:`--full` 时不起作用.

.. option:: -F, --full

   创建整个 Sphinx 项目, 与 :program:`sphinx-quickstart` 使用一样的机制.  
   大多数配置值被设置为默认，可通过下面选项去修改.

.. option:: -H project

   设置项目名 (查看 :confval:`project`).

.. option:: -A author

   设置作者名 (查看 :confval:`copyright`).

.. option:: -V version

   设置文档版本 (查看 :confval:`version`).

.. option:: -R release

   设置文档的发布版本 (查看 :confval:`release`).
