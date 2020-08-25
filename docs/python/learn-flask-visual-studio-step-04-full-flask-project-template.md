---
title: 学习 Visual Studio 中的 Flask 教程的第 4 步，Web 项目模板
titleSuffix: ''
description: Visual Studio 项目上下文中 Flask 基础知识的演练，具体介绍了 Flask Web 项目和 Flask/Jade Web 项目模板提供的功能。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: fa59197e584c6c8062c13354178f883b60b36442
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88250561"
---
# <a name="step-4-use-the-full-flask-web-project-template"></a>步骤 4：使用完整的 Flask Web 项目模板

上一步：[为静态文件提供服务、添加页面和使用模板继承](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)

通过在 Visual Studio 中的“空白 Flask 应用项目”模板上生成应用，你已经了解了 Flask 的基础知识，现在可以轻松地了解“Flask Web 项目”模板生成的更完整的应用。

在此步骤中，将执行以下操作：

> [!div class="checklist"]
> - 使用“Flask Web 项目”模板创建一个更完整的 Flask Web 应用并检查项目结构（步骤 4-1）
> - 了解由项目模板创建的视图和页面模板，该模板由三个继承自基本页面模板的页面组成，并使用 jQuery 和 Bootstrap 等静态 JavaScript 库（步骤 4-2）
> - 了解模板提供的 URL 路由（步骤 4-3）

本文也适用于“Flask/Jade Web 项目”模板，它生成的应用与使用 Jade 模板引擎（而不是 Jinja）的“Flask Web 项目”生成的应用相同。 文末包含更多详细信息。

## <a name="step-4-1-create-a-project-from-the-template"></a>步骤 4-1：通过模板创建项目

1. 在 Visual Studio 中，转到解决方案资源管理器，右键单击本教程中之前创建的“LearningFlask”解决方案，并选择“添加” > “新项目”。 （或者，如果想要使用新的解决方案，请改为选择“文件”   > “新建”   > “项目”  。）

1. 在“新建项目”对话框中，搜索并选择“Flask Web 项目”模板，调用项目“FlaskWeb”并选择“确定”   。

1. 因为模板再次包含 requirements.txt 文件，Visual Studio 会询问在何处安装这些依赖项  。 选择“安装到虚拟环境”  选项，然后在“添加虚拟环境”  对话框中，选择“创建”  以接受默认设置。

1. Visual Studio 完成虚拟环境的设置后，若要将“FlaskWeb”项目设置为 Visual Studio 解决方案的默认值，可以在解决方案资源管理器中右键单击该项目，然后选择“设为启动项目”    。 启动项目（以粗体显示）会在启动调试器时运行。

    ![将 FlaskWeb 项目显示为启动项目的解决方案资源管理器](media/flask/step04-second-project-in-solution-set-as-startup-project.png)

1. 选择“调试” > “启动调试”(F5) 或使用工具栏上的“Web 服务器”按钮运行服务器：

    ![Visual Studio 中的运行 Web 服务器工具栏按钮](media/flask/run-web-server-toolbar-button.png)

1. 该模板创建的应用有三个页面：“主页”、“关于”和“联系信息”，可以使用导航栏在其中进行导航。 花一到两分钟的时间检查应用的不同部分。 若要通过“登录”  命令对应用进行身份验证，请使用前面创建的超级用户凭据。

    ![Flask Web 项目应用的完整浏览器视图](media/flask/step04-full-app-desktop-view.png)

1. 由“Flask Web 项目”模板创建的应用将使用适用于响应式布局的 Bootstrap，以适应移动设备外形规格。 要查看此响应能力，可以将浏览器调整为窄视图，使内容垂直显示，并使导航栏变为菜单图标：

    ![Flask Web 项目应用的移动（窄）视图](media/flask/step04-full-app-mobile-view.png)

1. 可以在以下各节中使应用保持运行状态。

    若要停止应用并[将更改提交到源代码管理](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control)，首先打开团队资源管理器中的“更改”页，右键单击虚拟环境的文件夹（可能是 env），然后选择“忽略这些本地项”     。

### <a name="examine-what-the-template-creates"></a>检查模板创建的内容

“Flask Web 项目”模板创建以下结构。 这些内容与之前在步骤中创建的内容非常相似。 不同的是，“Flask Web 项目”模板在 static 文件夹中包含多个结构，因为它包含用于响应式设计的 jQuery 和 Bootstrap  。 该模板还将添加“联系人”页。 总体而言，如果已按照本教程中的前几个步骤操作，你应当熟悉模板中的所有内容。

- 项目根目录中的文件：
  - runserver.py，即开发服务器中运行应用的脚本  。
  - requirements.txt 包含了 Flask 0.x 上的依赖项  。
- FlaskWeb 文件夹包含所有应用文件  ：
  - \_\_init.py\_\_ 将应用代码标记为 Python 模块，创建 Flask 对象并导入应用的视图  。
  - views.py 包含了用于呈现页面的代码  。
  - Static 文件夹包含名为 content（CSS 文件）、fonts（字体文件）和 scripts（JavaScript 文件）的子文件夹     。
  - templates 文件夹包含 layout.html 基本模板以及每个扩展 layout.html 的特定网页的 about.html、contact.html 和 index.html       。

### <a name="question-is-it-possible-to-share-a-virtual-environment-between-visual-studio-projects"></a>问：能否能在 Visual Studio 项目之间共享虚拟环境？

答：可以，但在执行此操作时请注意，随着时间的推移，不同的项目可能会使用不同的包，因此共享的虚拟环境必须包含使用它的所有项目的所有包。

不过，若要使用现有的虚拟环境，需执行以下操作：

1. 当系统提示在 Visual Studio 中安装依赖项时，请选择“我将自行安装”  选项。
1. 在“解决方案资源管理器”  中，右键单击“Python 环境”  节点并选择“添加现有虚拟环境”  。
1. 导航到包含虚拟环境的文件夹并选中它，然后选择“确定”  。

## <a name="step-4-2-understand-the-views-and-page-templates-created-by-the-project-template"></a>步骤 4-2：了解通过项目模板创建的视图和页面模板

正如你在运行项目时所观察到的，该应用包含三个视图：“主页”、“关于”和“联系信息”。 这些视图的代码位于 FlaskWeb/views.py 文件夹中  。 每个视图函数只需借助指向模板的路径，以及提供给模板的值的参数变量列表即可调用 `flask.render_template`。 例如，`about` 函数（它的修饰器提供 URL 路由）处理“关于”页：

```python
@app.route('/about')
def about():
    """Renders the about page."""
    return render_template(
        'about.html',
        title='About',
        year=datetime.now().year,
        message='Your application description page.'
    )
```

`home` 和 `contact` 函数几乎完全相同，两者的装饰器类似，参数略有不同。

模板位于应用的 templates 文件夹中  。 基本模板 layout.html 的使用最为广泛  。 它指的是所有必需的静态文件（JavaScript 和 CSS），定义了其他页面覆盖的名为“内容”的块，并提供了另一个名为“脚本”的块。 以下来自 layout.html 的注释的摘录内容显示了这些特定区域  ：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <!-- Define a viewport for Bootstrap's responsive rendering -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title }} - My Flask Application</title>

    <link rel="stylesheet" type="text/css" href="/static/content/bootstrap.min.css" />
    <link rel="stylesheet" type="text/css" href="/static/content/site.css" />
    <script src="/static/scripts/modernizr-2.6.2.js"></script>
</head>

<body>
    <!-- Navbar omitted -->

    <div class="container body-content">
        <!-- "content" block that pages are expected to override -->
        {% block content %}{% endblock %}
        <hr />
        <footer>
            <p>&copy; {{ year }} - My Flask Application</p>
        </footer>
    </div>

    <!-- Additional scripts; use the "scripts" block to add page-specific scripts.  -->
    <script src="/static/scripts/jquery-1.10.2.js"></script>
    <script src="/static/scripts/bootstrap.js"></script>
    <script src="/static/scripts/respond.js"></script>
    {% block scripts %}{% endblock %}

</body>
</html>
```

每个单页模板 about.html、contact.html、index.html 均扩展了基本模板 layout.html     。 about.html 最简单，它显示 `{% extends %}` 和 `{% block content %}` 标记：

```html
{% extends "app/layout.html" %}

{% block content %}

<h2>{{ title }}.</h2>
<h3>{{ message }}</h3>

<p>Use this area to provide additional information.</p>

{% endblock %}
```

index.html 和 contact.html 使用相同的结构，在“内容”块中提供更长的内容   。

## <a name="the-flaskjade-web-project-template"></a>Flask/Jade Web 项目模板

如本文开头所述，Visual Studio 提供“Flask/Jade Web 项目”模板，该模板创建的应用程序与“Flask Web 项目”生成的应用程序在视觉上相同。 主要区别在于它使用 Jade 模板引擎，该引擎是 Jinja 的扩展，Jinja 使用更简洁的语言来实现相同的概念。 具体来说，例如，Jade 使用关键字而不是括在 {% %} 分隔符中的标记，使你可以使用关键字引用 CSS 样式和 HTML 元素。

要启用 Jade，项目模板首先在 requirements.txt 中包含 pyjade 包  。

该应用的 \_\_init\_\_.py 文件包含一行

```python
app.jinja_env.add_extension('pyjade.ext.jinja.PyJadeExtension')
```

在 templates 文件夹中，会看到 .jade 文件而不是 .html 模板，并且 views.py 中的视图在对 `flask.render_template` 的调用中引用这些文件。 否则，视图代码相同。

打开其中一个 .jade 文件，可以看到模板更简洁的表达式  。 例如，以下是由“Flask/Jade Web 项目”模板创建的 templates/layout.jade 的内容  ：

```jade
doctype html
html
  head
    meta(charset='utf-8')
    meta(name='viewport', content='width=device-width, initial-scale=1.0')
    title #{title} - My Flask/Jade Application
    link(rel='stylesheet', type='text/css', href='/static/content/bootstrap.min.css')
    link(rel='stylesheet', type='text/css', href='/static/content/site.css')
    script(src='/static/scripts/modernizr-2.6.2.js')
  body
    .navbar.navbar-inverse.navbar-fixed-top
      .container
        .navbar-header
          button.navbar-toggle(type='button', data-toggle='collapse', data-target='.navbar-collapse')
            span.icon-bar
            span.icon-bar
            span.icon-bar
          a.navbar-brand(href='/') Application name
        .navbar-collapse.collapse
          ul.nav.navbar-nav
            li
              a(href='/') Home
            li
              a(href='/about') About
            li
              a(href='/contact') Contact
    .container.body-content
      block content
      hr
      footer
        p &copy; #{year} - My Flask/Jade Application

    script(src='/static/scripts/jquery-1.10.2.js')
    script(src='/static/scripts/bootstrap.js')
    script(src='/static/scripts/respond.js')

    block scripts
```

以下是 templates/about.jade 的内容，显示了占位符的 `#{ <name>}` 用法：

```jade
extends layout

block content
  h2 #{title}.
  h3 #{message}
  p Use this area to provide additional information.
```

请随意试用 Jinja 和 Jade 语法，看看哪一个最适合。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [投票 Flask Web 项目模板](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md)

## <a name="go-deeper"></a>深入了解

- [编写你的第一个 Flask 应用，第 4 部分 - 窗体和通用视图](https://docs.djangoproject.com/en/2.0/intro/tutorial04/) (docs.djangoproject.com)
- [GitHub 上的 Jade（文档）](https://github.com/liuliqiang/pyjade)(github.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
