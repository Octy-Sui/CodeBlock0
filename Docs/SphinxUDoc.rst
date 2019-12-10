Sphinx使用手册
==================================================

探索Sphinx过程中的随笔记录，主要包含RST语言语法、Sphinx安装配置、目录检索兼容中文以及PythonAPI导出等部分内容。

RST语法
--------------------------------------------------

    | 详情见 :doc:`Template<../../template>`, 所见即所得，运行即可。

Sphinx安装配置
--------------------------------------------------

1.安装Sphinx

    .. code-block:: python

        pip install sphinx

2.配置Sphinx

    <1>. 为文档新建目录，并在该目录下运行

        .. code-block:: bat

            sphinx-quickstart

    <2>. 自定义配置选项，如下图所示
        | 根据项目情况自行选择,后续可在配置文件更改

        .. image::  ../../_static/images/Common/sphinx_config.JPG

        | 因为我们需要从Python代码的注释中自动导出API文档，
        | 所以需要将autodoc: automatically insert docstrings from modules (y/n) [n]: y
        | 如果忘记设置，可以在conf.py中的extensions中添加'sphinx.ext.autodoc'。
        | 选项后面没有输入的，直接按回车键使用默认设置。
        | 现在第一步所建目录下可见大致如下图，已配置选项不同，所有区别

        .. image::  ../../_static/images/Common/sphinx_demo.JPG

3.导出文档

    <1>. 导出API文档
        - config.py配置文件里修改指向代码路径
            | 相对路径

            .. code-block:: python

                import os
                import sys
                sys.path.insert(0, os.path.abspath('../../../src'))

            | 如上图所示
        - 生成toctree文件及rst文件
            | 在第二层sphinx_demo文件下执行

            .. code-block:: bat

                sphinx-apidoc -o source ..

            | 命令用法： usage: sphinx-apidoc [OPTIONS] -o <OUTPUT_PATH> <MODULE_PATH> [EXCLUDE_PATTERN, ...]
        - 清理文件

            .. code-block:: bat

                make clean

        - 导出文件

            .. code-block:: bat

                make html

    <2>. 生成技术文档
        - 与生成API文件不同，不用指向代码路径，注释掉即可。
        - 文档结构，参考本文档的设置，主要在于“.. toctree::”的使用
        - rst文件为手动书写，因而不必使用sphinx-apidoc命令
        - 清理文件

            .. code-block:: bat

                make clean

        - 导出文件

            .. code-block:: bat

                make html

中文目录检索
--------------------------------------------------

    1. 为使Sphinx支持中文检索，须在Sphinx源文件里做如下更改
        | **特别是当Sphinx库重新获取或升级后**
        | 在Root/Python/Lib/site_packages/sphinx/search/__init__.py做如下更改

        .. code-block:: python

            from sphinx.search.zh import SearchChinese
            # 新增导入中文检索方法

            languages = {
                            'da': 'sphinx.search.da.SearchDanish',
                            'de': 'sphinx.search.de.SearchGerman',
                            'en': SearchEnglish,
                            'es': 'sphinx.search.es.SearchSpanish',
                            'fi': 'sphinx.search.fi.SearchFinnish',
                            'fr': 'sphinx.search.fr.SearchFrench',
                            'hu': 'sphinx.search.hu.SearchHungarian',
                            'it': 'sphinx.search.it.SearchItalian',
                            'ja': 'sphinx.search.ja.SearchJapanese',
                            'nl': 'sphinx.search.nl.SearchDutch',
                            'no': 'sphinx.search.no.SearchNorwegian',
                            'pt': 'sphinx.search.pt.SearchPortuguese',
                            'ro': 'sphinx.search.ro.SearchRomanian',
                            'ru': 'sphinx.search.ru.SearchRussian',
                            'sv': 'sphinx.search.sv.SearchSwedish',
                            'tr': 'sphinx.search.tr.SearchTurkish',
                            'zh': SearchChinese,
                        }
                        # type: Dict[str, Any] 新增选项：'zh': SearchChinese

    2. 兼容中文检索，RST文件使用UTF-8编码
    3. notepad里可以转换文件的编码方式

:版本: 1.0
:日期: 12/05/2019
:作者: guangyuan.sui