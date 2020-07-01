---
title: 学习 Visual Studio 中的 Django 教程的第 3 步，静态文件和页面
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体演示了如何提供静态文件、将页面添加到应用，并使用模板继承
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: fc87c4690978d33f6fdc8e0f5bc937cb16e6e915
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85279804"
---
# <a name="step-3-serve-static-files-add-pages-and-use-template-inheritance"></a>步骤 3：提供静态文件、添加页面和使用模板继承

**上一步：[使用视图和页面模板创建 Django 应用](learn-django-in-visual-studio-step-02-create-an-app.md)**

在本教程的前几个步骤中，你已了解如何在自包含 HTML 的单个页面中创建最小的 Django 应用。 然而，现代 Web 应用通常由许多页面组成，并利用 CSS、JavaScript 文件等共享资源来提供一致的样式和行为。

在此步骤中，你将了解如何：

> [!div class="checklist"]
> - 使用 Visual Studio 项模板快速添加具有方便样本代码的不同类型的新文件（步骤 3-1）
> - 配置 Django 项目来提供静态文件（步骤 3-2）
> - 向应用添加其他页（步骤 3-3）
> - 使用模板继承创建跨页使用的标头和导航栏（步骤 3-4）

## <a name="step-3-1-become-familiar-with-item-templates"></a>步骤 3-1：熟悉项模板

在开发 Django 应用时，通常会添加更多的 Python、HTML、CSS 和 JavaScript 文件。 对于每个文件类型（以及诸如 web.config 等其他需要部署的文件），Visual Studio 提供了方便的[项模板](python-item-templates.md)来帮助入门。

若要查看可用模板，请转到“解决方案资源管理器”，右键单击要在其中创建项的文件夹，选择“添加” > “新项”：

![Visual Studio 中的“添加新项”对话框](media/django/step03-add-new-item-dialog.png)

若要使用模板，选择所需的模板，为该文件指定一个名称，然后选择“确定”。 以这种方式添加项会自动将文件添加到 Visual Studio 项目中，并标记对源代码管理所做的更改。

### <a name="question-how-does-visual-studio-know-which-item-templates-to-offer"></a>问：Visual Studio 如何知道要提供哪些项模板？

答：Visual Studio 项目文件 (.pyproj) 包含一个项目类型标识符，它将其标记为 Python 项目。 Visual Studio 使用此类型标识符来仅显示那些适用于项目类型的项模板。 通过这种方式，Visual Studio 可以为许多项目类型提供一组丰富的项模板，而不必每次都要求你对它们进行排序。

## <a name="step-3-2-serve-static-files-from-your-app"></a>步骤 3-2：从应用中提供静态文件

在使用 Python（借助任何框架）生成的 Web 应用中，Python 文件始终在 Web 主机的服务器上运行，并且永远不会传输到用户计算机。 然而，其他文件（如 CSS 和 JavaScript）都是由浏览器专用的，因此，主机服务器会在需要时按原样传递它们。 此类文件称为“静态”文件，无需你编写任何代码，Django 可以自动交付它们。

Django 项目默认配置为从应用的 static 文件夹中提供静态文件，这要归功于 Django 项目的 settings.py 中的以下行 ：

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/

STATIC_URL = '/static/'

STATIC_ROOT = posixpath.join(*(BASE_DIR.split(os.path.sep) + ['static']))
```

可使用 static 中你喜欢的任意文件夹结构来组织文件，然后在该文件夹中使用相对路径来引用文件。 为了演示此过程，下面的步骤会将 CSS 文件添加到应用中，然后在 index.html 模板中使用该样式表：

1. 在解决方案资源管理器中，右键单击 Visual Studio 项目中的“HelloDjangoApp”文件夹，依次选择“添加” > “新文件夹”，并命名文件夹 `static`   。

1. 右键单击 static 文件夹，然后选择“添加” > “新项”  。 在出现的对话框中，选择“样式表”模板，将文件命名为 `site.css`，然后选择“确定” 。 site.css 文件出现在项目中，并在编辑器中打开。 文件夹结构应类似于下图：

    ![解决方案资源管理器中显示的静态文件结构](media/django/step03-static-file-structure.png)

1. 将 site.css 的内容替换为以下代码并保存文件：

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. 将应用的 templates/HelloDjangoApp/index.html 文件的内容替换为以下代码，从而将步骤 2 中使用的 `<strong>` 元素替换为引用 `message` 样式类的 `<span>`。 通过此方式使用样式类为设计元素样式提供了更多灵活性。 （如果在使用 VS 2017 15.7 及更早版本时，尚未将 index.html 移动到 templates 的子文件夹中，请参阅步骤 2-4 中的[模板命名空间](learn-django-in-visual-studio-step-02-create-an-app.md#template-namespacing) 。）

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load staticfiles %} <!-- Instruct Django to load static files -->
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <span class="message">{{ message }}</span>{{ content }}
        </body>
    </html>
    ```

1. 运行项目以观察结果。 完成后停止服务器，根据需要将更改提交到源代码管理（如[步骤 2](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control) 中所述）。

### <a name="question-what-is-the-purpose-of-the--load-staticfiles--tag"></a>问：{% load staticfiles %} 标记的用途是什么？

答：在指示像 `<head>` 和 `<body>` 这样的元素中的静态文件之前，需要使用 `{% load staticfiles %}` 行。 本节所示的示例中，“staticfiles”指的是自定义 Django 模板标记集，它允许使用 `{% static %}` 语法来引用静态文件。  如果没有 `{% load staticfiles %}`，那么在应用运行时，将看到异常。

### <a name="question-are-there-any-conventions-for-organizing-static-files"></a>问：是否有组织静态文件的任何约定？

答：可以在 static 文件夹中以所需的方式添加其他 CSS、JavaScript 和 HTML 文件。 组织静态文件的一种典型方法是创建名为 fonts、scripts 和 content 的子文件夹（用于样式表和任何其他文件）  。 在每一种情况下，请记住要将这些文件夹包含在指向 `{% static %}` 引用中文件的相对路径中。

### <a name="question-can-i-complete-the-same-task-without-using-the--load-staticfiles--tag"></a>问：是否可以在不使用 {% load staticfiles %} 标记的情况下完成相同任务？

答：可以。

```html
<html>
    <head>
        <title>{{ title }}</title>
        <link rel="stylesheet" type="text/css" href="../../static/site.css" />
    </head>
    <body>
        <span class="message">{{ message }}</span>{{ content }}
    </body>
</html>
```

## <a name="step-3-3-add-a-page-to-the-app"></a>步骤 3-3：向应用添加一个页面

将其他页添加到应用意味着：

- 添加用于定义视图的 Python 函数。
- 添加用于页面标记的模板。
- 将必需的路由添加到 Django 项目的 urls.py 文件中。

以下步骤将“关于”页面添加到“HelloDjangoApp”项目，并从主页链接到该页面：

1. 在解决方案资源管理器中，右键单击 templates/HelloDjangoApp 文件夹，选择“添加” > “新项”，选择“HTML 页”项模板，将文件命名为 `about.html`，然后选择“确定”     。

    > [!Tip]
    > 如果“新项”命令未显示在“添加”菜单上，请确保已停止服务器，使 Visual Studio 退出调试模式。

1. 用下面的标记替换 about.html 的内容（可以在步骤 3-4 中使用简单的导航栏替换到主页的显式链接）：

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load staticfiles %}
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <div><a href="home">Home</a></div>
            {{ content }}
        </body>
    </html>
    ```

1. 打开应用的 views.py 文件，并添加使用该模板的名为 `about` 的函数：

    ```python
    def about(request):
        return render(
            request,
            "HelloDjangoApp/about.html",
            {
                'title' : "About HelloDjangoApp",
                'content' : "Example app page for Django."
            }
        )
    ```

1. 打开 Django 项目的 urls.py 文件，将以下行添加到 `urlPatterns` 数组：

    ```python
    url(r'^about$', HelloDjangoApp.views.about, name='about'),
    ```

1. 打开 templates/HelloDjangoApp/index.html 文件，添加 `<body>` 元素下的以下行以链接到“关于”页（同样，可以使用步骤 3-4 中的导航栏替换此链接）：

    ```html
    <div><a href="about">About</a></div>
    ```

1. 若要保存所有文件，请使用“文件” > “全部保存”菜单命令，或只需按 Ctrl+Shift+S    。 （从技术上讲，不需要执行此步骤，因为在 Visual Studio 中运行项目会自动保存文件。 不过，可以了解一下这个命令！）

1. 运行项目并观察结果，并检查页面之间的导航。 完成时关闭服务器。

### <a name="question-i-tried-using-index-for-the-link-to-the-home-page-but-it-didnt-work-why"></a>问：我曾尝试使用“index”来链接到主页，但它不起作用。 为什么？

答：即使“views.py”中的视图函数被命名为 `index`，Django 项目“urls.py”文件中的 URL 路由模式也不包含与字符串“index”相匹配的正则表达式 。 若要匹配该字符串，需要为模式 `^index$` 添加另一个条目。

如下一节所示，最好在页面模板中使用 `{% url '<pattern_name>' %}` 标记来引用模式的名称，在这种情况下，Django 会为你创建适当的 URL。 例如，用 `<div><a href="{% url 'index' %}">Home</a></div>` 替换 about.html 中的 `<div><a href="home">Home</a></div>`。 在这里使用“index”会起作用，因为 urls.py 中的第一个 URL 模式实际上被命名为“index”（依据 `name='index'` 参数）。 也可以用“home”来引用第二种模式。

## <a name="step-3-4-use-template-inheritance-to-create-a-header-and-nav-bar"></a>步骤 3-4：使用模板继承创建标头和导航栏

与在每个页面上都有显式导航链接不同，现代 Web 应用通常使用品牌标头和提供最重要的页面链接、弹出菜单等内容的导航栏。 确保标头和导航栏在所有页面中都相同，但是你不希望在每个页面模板中重复相同的代码。 相反，你希望在一个位置定义所有页面的公共部分。

Django 模板系统为实现跨多个模板重用特定元素提供了两种方法：包含和继承。

- 包含是可以使用语法 `{% include <template_path> %}` 在引用模板的特定位置插入的另一个页面模板。 如果想要在代码中动态更改路径，也可以使用一个变量。 包含通常用于页面主体，在页面特定位置拉入共享模板。

- 继承使用页面模板开头的 `{% extends <template_path> %}` 来指定共享基本模板，然后会在此模板上生成引用模板。 继承通常用于为应用页面定义共享布局、导航栏和其他结构，这样一来，引用模板只需要添加或修改称为“块”的基本模板的特定区域。

在这两种情况下，`<template_path>` 对应于应用的 templates 文件夹（还允许 `../` 或 `./`）。

基本模板使用 `{% block <block_name> %}` 和 `{% endblock %}` 标记来标示块。 如果引用模板随后使用具有相同块名称的标记，那么它的块内容将替代基本模板的内容。

以下步骤演示继承：

1. 在应用的 templates/HelloDjangoApp 文件夹中，新建一个名为 layout.html 的 HTML 文件（使用“添加” > “新项”上下文菜单或“添加” > “HTML 页”），再将其内容替换为以下标记   。 可以看到此模板包含一个名为“content”的块，这是引用页面需要替换的全部内容：

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>{{ title }}</title>
        {% load staticfiles %}
        <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
    </head>

    <body>
        <div class="navbar">
           <a href="/" class="navbar-brand">Hello Django</a>
           <a href="{% url 'home' %}" class="navbar-item">Home</a>
           <a href="{% url 'about' %}" class="navbar-item">About</a>
        </div>

        <div class="body-content">
    {% block content %}{% endblock %}
            <hr/>
            <footer>
                <p>&copy; 2018</p>
            </footer>
        </div>
    </body>
    </html>
    ```

1. 向应用的 static/site.css 文件添加以下样式（本教程不会尝试在此处演示响应式设计；这些样式仅仅是为了生成一个有趣的结果）：

    ```css
    .navbar {
        background-color: lightslategray;
        font-size: 1em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        color: white;
        padding: 8px 5px 8px 5px;
    }

    .navbar a {
        text-decoration: none;
        color: inherit;
    }

    .navbar-brand {
        font-size: 1.2em;
        font-weight: 600;
    }

    .navbar-item {
        font-variant: small-caps;
        margin-left: 30px;
    }

    .body-content {
        padding: 5px;
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    ```

1. 修改 templates/HelloDjangoApp/index.html 以引用基本模板并替换内容块。 可以看到，通过使用继承，此模板变得很简单：

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    <span class="message">{{ message }}</span>{{ content }}
    {% endblock %}
    ```

1. 修改 templates/HelloDjangoApp/about.html 也可以引用基本模板并替换内容块：

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    {{ content }}
    {% endblock %}
    ```

1. 运行服务器并观察结果。 完成时关闭服务器。

    ![显示导航栏的正在运行的应用](media/django/step03-nav-bar.png)

1. 你已经对应用进行了大幅更改，现在是[将所做的更改提交到源代码管理](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)的好时机。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用完整的 Django Web 项目模板](learn-django-in-visual-studio-step-04-full-django-project-template.md)

## <a name="go-deeper"></a>深入了解

- [将 Web 应用部署到 Azure App Service](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [编写你的第一个 Django 应用，第 3 部分（视图）](https://docs.djangoproject.com/en/2.0/intro/tutorial03/) (docs.djangoproject.com)
- 有关 Django 模板的更多功能（如控制流），请参阅 [Django 模板语言](https://docs.djangoproject.com/en/2.0/ref/templates/language/) (docs.djangoproject.com)
- 有关使用 `{% url %}` 标记的完整详细信息，请参阅 [Django 模板的内置模板标记和筛选器参考](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/)中的 [URL](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/#url) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
