DocString Format
==================================================

为便于输出有效的代码文档，按一致的规则书写注释，有助于大家理解。
本文主要包含模块注释、类注释、函数注释等三部分。

DocString
--------------------------------------------------

    | Python有一种独一无二的的注释方式: 使用文档字符串. 文档字符串是包, 模块, 类或函数里的第一个语句.
    | 这些字符串可以通过对象的__doc__成员被自动提取, 并且被pydoc所用. (你可以在你的模块上运行pydoc试一把, 看看它长什么样).
    | 我们对文档字符串的惯例是使用三重双引号""""""( PEP-257_ ).
    | 一个文档字符串应该这样组织: 首先是一行以句号, 问号或惊叹号结尾的概述(或者该文档字符串单纯只有一行).接着是一个空行.
    | 接着是文档字符串剩下的部分, 它应该与文档字符串的第一行的第一个引号对齐.
    | 下面有更多文档字符串的格式化规范.

    .. _PEP-257: https://www.python.org/dev/peps/pep-0257/#what-is-a-docstring

模块注释
--------------------------------------------------

    | 每个文件应该包含一个许可样板. 根据项目使用的许可(例如, Apache 2.0, BSD, LGPL, GPL), 选择合适的样板.
    | 除此之外，记录模块的 **功能** 、大致 **描述** 以及 **使用方法** 等。如下

    .. code-block:: python

        # _*_ coding:utf-8 _*_

        """A one line summary of the module or program, terminated by a period.

        Leave one blank line.  The rest of this docstring should contain an
        overall description of the module or program.  Optionally, it may also
        contain a brief description of exported classes and functions and/or usage
        examples.

          Typical usage example:

          foo = ClassFoo()
          bar = foo.FunctionBar()
        """

类注释
--------------------------------------------------

    类应该在其定义下有一个用于描述该类的文档字符串. 如果你的类有 **公共属性** (Attributes),
    那么文档中应该有一个属性(Attributes)段. 并且应该遵守和函数参数相同的格式.

    | 属性名name记得使用":name:"来定义并高亮显示

    .. code-block:: python

        class SampleClass(object):
        """Summary of class here.

        Longer class information....
        Longer class information....

        Attributes:
            :likes_spam: A boolean indicating if we like SPAM or not.
            :eggs: An integer count of the eggs we have laid.
        """

        def __init__(self, likes_spam=False):
            """Inits SampleClass with blah."""
            self.likes_spam = likes_spam
            self.eggs = 0

        def public_method(self):
            """Performs operation blah."""

函数注释
--------------------------------------------------

    下文所指的函数,包括函数, 方法, 以及生成器.

    一个函数必须要有文档字符串, 除非它满足以下条件:
        + 外部不可见
        + 非常短小
        + 简单明了

    文档字符串应该包含函数做什么, 以及输入和输出的详细描述. 通常, 不应该描述”怎么做”, 除非是一些复杂的算法.

    文档字符串应该提供足够的信息, 当别人编写代码调用该函数时, 他不需要看一行代码, 只要看文档字符串就可以了.

    对于复杂的代码, 在代码旁边加注释会比使用文档字符串更有意义.

    关于函数的几个方面应该在特定的小节中进行描述记录.

    1. Args

        | 列出每个参数的名字, 并在名字前使用一个冒号，名字后使用一个冒号和一个空格, 分隔对该参数的描述.
        | 如果描述太长超过了单行80字符,使用2或者4个空格的悬挂缩进(与文件其他部分保持一致). 描述应该包括所需的类型和含义.
        | 如果一个函数接受*foo(可变长度参数列表)或者**bar (任意关键字参数), 应该详细列出*foo和**bar.

    2. Returns

        描述返回值的类型和语义. 如果函数返回None, 这一部分可以省略.

    3. Raises

        列出与接口有关的所有异常.

    4. Format
        | 采用更普遍格式是Sphinx用于生成文档的reStructureText(reST)格式
        | 默认情况，在PyCharm定义方法后，键入三引号并按Enter键会输出格式模板.
        | 不幸关闭了，设置位置Tools->Python Integrated Tools->Docstrings->Docstring format; 选择reStructuredText模式

        .. code-block:: python

            def public_method(a=1, b):
                """
                A short description of function. Behind of it, a blank line is must!

                :param str a: description of a.(default 1)
                :param list b: description of b.
                :return: this is a description of what it returns
                :raises keyError: description of when to raise exception
                """
                ...
                pass

DocString注意事项
--------------------------------------------------

    1. 只会输出本层级内第一个""""""内的内容。
    2. 只导出公共方法的docstring; 如果有的方法或函数不想输出，可定义为私有。
    3. __init__内的注释不会导出

DemoOfDocString
--------------------------------------------------

    .. code-block:: python

        # _*_ coding:utf-8 _*_

        """A one line summary of the module or program, terminated by a period.

        Leave one blank line.  The rest of this docstring should contain an
        overall description of the module or program.  Optionally, it may also
        contain a brief description of exported classes and functions and/or usage
        examples.

          Typical usage example:

          foo = SampleClass()
          bar = foo.public_method()
        """


        class SampleClass(object):
            """Summary of class here.

            Longer class information....
            Longer class information....

            Attributes:
                :likes_spam: A boolean indicating if we like SPAM or not.
                :eggs: An integer count of the eggs we have laid.
            """

            def __init__(self, likes_spam=False):
                """Inits SampleClass with blah."""
                self.likes_spam = likes_spam
                self.eggs = 0

            def public_method(self, b, a=1):
                """
                A short description of function. Behind of it, a blank line is must!

                :param str a: description of a.(default 1)
                :param list b: description of b.
                :return: this is a description of what it returns
                :raises TypeError: description of when to raise exception
                :raises KeyError: description of when to raise exception
                """
                i = a
                j =  b
                """hello world"""
                if not isinstance(a, str):
                    raise TypeError
                return i, j

            def _private_method(self, b, a=1):
                """
                A short description of function. Behind of it, a blank line is must!

                :param str a: description of a.(default 1)
                :param list b: description of b.
                :return: this is a description of what it returns
                :raises TypeError: description of when to raise exception
                :raises KeyError: description of when to raise exception
                """
                i = a
                j =  b
                if not isinstance(a, str):
                    raise TypeError
                return i, j

            def one_line_docs(self):
                """one line docstring"""
                pass

            def no_docs(self):
                pass

    **最终文档效果**

    .. image::  ../../_static/images/Common/demo_docstring.JPG

参考文档

    1. `PEP257 <https://www.python.org/dev/peps/pep-0257/#what-is-a-docstring>`_
    2. `什么是标准的Python文档字符串格式? <https://codeday.me/bug/20190915/1805376.html>`_
    3. `Google Python 风格指南 <https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/>`_

:版本: 1.0
:日期: 12/06/2019
:作者: guangyuan.sui