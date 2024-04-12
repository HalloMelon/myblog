## Mkdocs 配置和使用
MkDocs是一个快速、简单、华丽的静态网站生成器，适用于构建项目文档。文档源文件以Markdown编写，并使用一个YAML文件来进行配置。 MkDocs生成完全静态的HTML网站，你可以将其部署到GitHub pages、Amzzon S3或你自己选择的其它任意地方。

- 官方地址：https://www.mkdocs.org/
- 中文文档地址：https://mkdocs.zimoapps.com/

MkDocs有一堆很好看的主题。 官方内置了两个主题： mkdocs 和readthedocs， 也可以从MkDocs wiki中选择第三方主题， 或者自定义主题。

### 安装
Mkdocs是用Python开发的工具可以使用pip命令来安装
```
pip install mkdocs
```
### 使用
在本地建立一个my-project文件夹　其中包括了一个mkdocs.yml和一个docs文件夹
```
mkdocs new my-project
```

- mkdocs.yml: 这个文件是一个配置文件主要配置你的站点名字，板块等具体配置
- docs: 是存放你要写的 Markdown 文档的地方初始化一个index.md文档配置

在本地查看搭建的文档效果,访问`http://127.0.0.1:8000/`就可以看到生成文档的效果了
```
mkdocs serve
Running at: http://127.0.0.1:8000/
```
### material主题
这个主题更加强大一点，比如它支持中文全局搜索。

首先安装主题和一些常用插件，比如导出pdf

```
# 第一步先下载安装gtk3-runtime-3.xxx-ts-win64.exe，去下面的路径下载最新的然后安装
# https://github.com/tschoonj/GTK-for-Windows-Runtime-Environment-Installer/releases
pip install --upgrade setuptools
pip install mkdocs-material
#pip install mkdocs-pdf-export-plugin #这个插件有点晚问题，等它更新了再玩
```

注意：安装tgk3后，自动会将它的bin加入到PATH中，但是后面运行的时候回出现异常cannot load library 'libcairo.so':。 解决办法是将这个bin路径放到PATH的第一个位置即可。太机智了

#### 完整配置


```

site_name: 'core-algorithm'
site_author: '熊能'
site_description: '看我七十二变'
site_url: 'https://www.xncoding.com/'
copyright: Copyright © 2020 XiongNeng

# 源码地址
#repo_name: 'yidao620c/core-algorithm'
#repo_url: 'https://github.com/yidao620c/core-algorithm'
#edit_uri: 'blob/master/docs/'

nav:
- Index: index.md
- Documents:
  - 第一部分:
    - 数据结构: chapters/chapter1/post01.md
    - IO操作: chapters/chapter1/post02.md
  - 第二部分:
    - 多线程: chapters/chapter2/post03.md
    - 面向对象编程: chapters/chapter2/post04.md
    - 网络编程: chapters/chapter2/post05.md
    - 备忘录:
        - 我爱你: chapters/chapter2/temp/temp01.md
        - 买个锤子: chapters/chapter2/temp/temp02.md
- 关于我们:
  - About: about.md

#主题
theme:
  name: 'material'
  language: 'zh'  # 配置语言
  palette:  # 颜色
    primary: 'light blue'
    accent: 'indigo'
  feature:
    tabs: true  # 横向导航
  custom_dir: 'docs/resources/'

markdown_extensions:
  - admonition  # 提示块
  - footnotes  # 脚注
  - meta  # 定义元数据，通过文章上下文控制，如disqus
  - pymdownx.caret  # 下划线上标
  - pymdownx.tilde  # 删除线下标
  - pymdownx.critic  # 增加删除修改高亮注释，可修饰行内或段落
  - pymdownx.details  # 提示块可折叠
  - pymdownx.inlinehilite  # 行内代码高亮
  - pymdownx.mark  # 文本高亮
  - pymdownx.smartsymbols  # 符号转换
  - pymdownx.superfences  # 代码嵌套在列表里
  - codehilite:    # 代码高亮，显示行号
      guess_lang: false
      linenums: true
  - toc:  # 锚点
      permalink: true
#  - pymdownx.arithmatex  # 数学公式
  - pymdownx.betterem:  # 对加粗和斜体更好的检测
      smart_enable: all
#  - pymdownx.emoji:  # 表情
#      emoji_generator: !!python/name:pymdownx.emoji.to_svg
#  - pymdownx.magiclink  # 自动识别超链接
  - pymdownx.tasklist:  # 复选框checklist
      custom_checkbox: true

# PDF导出插件
plugins:
  - search
#  - pdf-export #这个插件还有点问题，没有更新

#扩展样式
extra_css:
  - resources/css/extra.css

```

这里说明一下`tabs: true # 横向导航`，material主题支持将一级横向和二级纵向导航。 默认为false表示只支持左边纵向导航，效果也不错。如果是手机小屏幕则可以选择此选项。如果文档是写给电脑大屏看的， 则可以设置为true，这时候根据nav的设置分成两级导航。注意的是对于nav中的所有一级页面全部归属为一个组。 就是刚进来的index.md这个组，如果你不设置index.md主页，则这个组就看不到了。所以一定要有一个index.md的链接。

extra.css示例  
比如我想自定义表头的背景颜色。可通过F12查看源码，把原来的css定义复制到`docs/resource/css/extra.css`下，再修改下

```
.md-typeset table:not([class]) th {
    min-width: 5rem;
    padding: .6rem .8rem;
    background-color: #9facf6;
    color: #fff;
    vertical-align: top;
}
```

### 语法习惯
- 使用H1做title
- 文本修饰（带 ^^下划线^^ 的可修饰行内或段落）
- 加粗 bold
- 斜体字 斜体字
- 加粗斜体 粗斜体
- 下划线 ^^Insert me^^
- 删除线 Delete me
- 增加 {++ add ++}
- 修改 {~ is ~> are ~}
- 删除 {– del –}
- 高亮 {== highlight ==}
- 注释 {>> comment <<}
- 上标 H^2^O, text^a\ superscript^
- 下标 CH3CH2OH, texta\ subscript
- 行内代码高亮：:::java System.out.println("hello"); or #!python println('hello')
- 键盘快捷键标签：++ctrl+alt+f++