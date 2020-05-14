---
title: 了解 Visual Studio 中的 Django 教程步骤 2，视图和页面模板
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了创建应用以及使用视图和模板的步骤。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 5befdfb5f6974ff7b042319121a27c3628757b6e
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "79300887"
---
# <a name="step-2-create-a-django-app-with-views-and-page-templates"></a>步骤 2：使用视图和页面模板创建 Django 应用

**上一步：[创建 Visual Studio 项目和解决方案](learn-django-in-visual-studio-step-01-project-and-solution.md)**

到目前为止，在 Visual Studio 项目中，你所拥有的只是 Django 项目  的网站级组件，这些组件可以运行一个或多个 Django 应用  。 下一步是在单个页面中创建你的第一个应用。

在此步骤中，可以了解如何：

> [!div class="checklist"]
> - 在单个页面中创建 Django 应用（步骤 2-1）
> - 从 Django 项目运行应用（步骤 2-2）
> - 使用 HTML 呈现视图（步骤 2-3）
> - 使用 Django 页面模板呈现视图（步骤 2-4）

## <a name="step-2-1-create-an-app-with-a-default-structure"></a>步骤 2-1：创建具有默认结构的应用

Django 应用是一个单独的 Python 包，其中包含一组用于特定用途的相关文件。 一个 Django 项目可以包含任意数量的应用，这反映了一个事实：Web 主机可用于满足单个域名中任意数量的单独入口点。 例如，像 contoso.com 这样的域的 Django 项目可能包含一个面向 `www.contoso.com` 的应用、一个面向 support.contoso.com 的应用以及一个面向 docs.contoso.com 的应用。 在这种情况下，Django 项目处理网站级 URL 路由和设置（在其 urls.py 和 settings.py 文件中），同时每个应用在其内部路由、视图、模型、静态文件和管理界面中都有其自己的不同样式和行为   。

Django 应用通常以一组标准文件开始。 Visual Studio 提供项模板来初始化 Django 项目中的 Django 应用，并提供起到相同作用的集成菜单命令：

- 模板：在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新项”    。 在“添加新项”对话框中，选择“Django 1.9 应用”模板，在“名称”字段中指定应用名称，并选择“确定”     。

- 集成的命令：在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “Django 应用”    。 此命令将提示你输入一个名称，并创建 Django 1.9 应用。

    ![添加 Django 应用的菜单命令](media/django/step02-add-django-app-command.png)

使用任一方法创建一个名为“HelloDjangoApp”的应用。 其结果是项目中存在一个具有该名称的文件夹，其中包含下表中所述的项。

![解决方案资源管理器中的 Django 应用文件](media/django/step02-django-app-in-solution-explorer.png)

| 项 | 描述 |
| --- | --- |
| **\_\_init\_\_.py** | 将应用标识为包的文件。 |
| **迁移** | 一个文件夹，Django 在其中存储用于更新数据库以便与模型更改保持一致的脚本。 然后，Django 迁移工具将必要的更改应用到任何以前版本的数据库，以便与当前模型相匹配。 使用迁移，可以将注意力集中在模型上，并让 Django 处理基础数据库架构。 步骤 6 中已对迁移进行了讨论；现在，该文件夹只需包含 \_\_init\_\_.py 文件（指示文件夹定义其自己的 Python 包）  。 |
| **模板** | Django 页面模板文件夹，其中包含与应用名匹配的文件夹中的一个 index.html 文件  。 （在 Visual Studio 2017 15.7 及更早版本中，该文件直接包含在模板中，步骤 2-4 指示你创建子文件夹  。）模板是若干个 HTML 块，视图可以将信息添加到其中并以动态方式呈现页面。 页面模板“变量”（如 index.html 中的 `{{ content }}`）都是动态值占位符，如本文后面所述（步骤 2）  。 通常情况下，Django 应用通过将模板放置在与应用名称匹配的子文件夹中来创建其模板的命名空间。 |
| **admin.py** | 在其中扩展应用管理界面的 Python 文件（请参阅步骤 6），用于对数据库中的数据进行种子设定和编辑。 最初，此文件仅包含语句 `from django.contrib import admin`。 默认情况下，Django 在 Django 项目 settings.py 文件中的条目中包含一个标准的管理界面，可以通过取消评论 urls.py 中的现有条目将其打开   。 |
| **apps.py** | 定义应用配置类的 Python 文件（参见下文，在此表后）。 |
| **models.py** | 模型是由函数识别的数据对象，视图通过模型与应用的基础数据库进行交互（请参阅步骤 6）。 Django 提供数据库连接层，这样应用就无需考虑这些细节。 models.py 文件是用于创建模型的默认位置，最初只包含语句 `from django.db import models`  。 |
| **tests.py** | 包含单元测试基本结构的 Python 文件。 |
| **views.py** | 视图是你通常将其视为网页的对象，它接收 HTTP 请求并返回 HTTP 响应。 视图通常呈现为 Web 浏览器知道如何显示的 HTML，但视图不一定可见（比如中间形式）。 视图由 Python 函数定义，它的职责是呈现 HTML 以发送到浏览器。 views.py 文件是用于创建视图的默认位置，最初只包含语句 `from django.shortcuts import render`  。 |

使用名称“HelloDjangoApp”时，apps.py 内容如下所示  ：

```python
from django.apps import AppConfig

class HelloDjangoAppConfig(AppConfig):
    name = 'HelloDjango'
```

### <a name="question-is-creating-a-django-app-in-visual-studio-any-different-from-creating-an-app-on-the-command-line"></a>问：在 Visual Studio 中创建 Django 应用与在命令行上创建应用有什么不同吗？

答：运行“添加” > “Django 应用”命令或者将“添加” > “新项”与 Django 应用模板结合使用生成的文件与使用 Django 命令 `manage.py startapp <app_name>` 生成的文件相同     。 在 Visual Studio 中创建应用的好处是，应用文件夹及其所有文件都会自动集成到项目中。 可以使用相同的 Visual Studio 命令在项目中创建任意数量的应用。

## <a name="step-2-2-run-the-app-from-the-django-project"></a>步骤 2-2：从 Django 项目运行应用

此时，如果再次在 Visual Studio 中运行项目（使用工具栏按钮或”调试”   > “启动调试”  ），仍会看到默认页。 不会显示应用内容，因为需要定义一个特定于应用的页面，并将该应用添加到 Django 项目中：

1. 在 HelloDjangoApp 文件夹中，修改 views.py 以匹配以下代码，它定义名为“index”的视图   ：

    ```python
    from django.shortcuts import render
    from django.http import HttpResponse

    def index(request):
        return HttpResponse("Hello, Django!")
    ```

1. 在 BasicProject 文件夹（在步骤 1 中创建），修改 urls.py 以至少匹配以下代码（如果愿意，可保留有意义的注释）   ：

    ```python
    from django.conf.urls import include, url
    import HelloDjangoApp.views

    # Django processes URL patterns in the order they appear in the array
    urlpatterns = [
        url(r'^$', HelloDjangoApp.views.index, name='index'),
        url(r'^home$', HelloDjangoApp.views.index, name='home'),
    ]
    ```

    每个 URL 模式均介绍了 Django 向其路由特定网站对应的 URL 的视图（即“`https://www.domain.com/`”后面的部分）。 `urlPatterns` 中以正则表达式 `^$` 开头的第一个条目是站点根目录“/”的路由。 第二个条目 `^home$` 专门路由“/home”。 可以拥有到同一个视图的任意数量的路由。

1. 再次运行该项目并看到消息“Hello, Django!”  与视图定义的一致。 完成后，请停止服务器。

### <a name="commit-to-source-control"></a>提交到源代码管理

你已经对代码进行了更改并成功对其进行了测试，现在可以开始审阅更改并将其提交到源代码管理。 本教程中的后续步骤会在合适的时机提醒你再次提交到源代码管理，指引你回到本节。

1. 在 Visual Studio 底部选择“更改”按钮（下面的圆圈），可以导航到“团队资源管理器”  。

    ![Visual Studio 状态栏上的源代码管理更改按钮](media/django/step02-source-control-changes-button.png)

1. 在“团队资源管理器”  中，输入提交消息，如“创建初始 Django 应用”并选择“全部提交”  。 提交完成后，将看到一条消息“提交已在本地创建的 \<哈希>。  同步后与服务器共享你的更改。” 如果要将更改推送到远程存储库，请选择“同步”  ，然后选择“传出提交”  下的“推送”  。 在推送至远程存储库之前，还可以累积多个本地提交。

    ![将提交推送到团队资源管理器中的远程存储库](media/django/step02-source-control-push-to-remote.png)

### <a name="question-what-is-the-r-prefix-before-the-routing-strings-for"></a>问：路由字符串前的“r”前缀代表什么？

答：Python 中字符串的“r”前缀表示“raw”，它指示 Python 不转义字符串中的任何字符。 因为正则表达式使用许多特殊字符，相比包含许多“\\”转义字符，使用“r”前缀可以使这些字符串更易于读取。

### <a name="question-what-do-the--and--characters-mean-in-the-url-routing-entries"></a>问：在 URL 路由条目中，^ 和 $ 字符表示什么意思？

答：在定义 URL 模式的正则表达式中，^ 表示“行开头”，而 $ 则表示“行结尾”，其中 URL 再次对应站点根目录（`https://www.domain.com/` 后面的部分）。 正则表达式 `^$` 实际上表示“空白”，因此匹配完整 URL `https://www.domain.com/`（不会向站点根目录添加任何内容）。 模式 `^home$` 精确匹配 `https://www.domain.com/home/`。 （Django 不在模式匹配中使用尾随 /。）

如果在正则表达式中不使用尾随 $，比如 `^home`，那么 URL 模式匹配任何  以“home”开头的 URL，如“home”、“homework”、“homestead”和“home192837”。

若要尝试使用不同的正则表达式，请尝试使用联机工具，如 [pythex.org](https://www.pythex.org) 中的 [regex101.com](https://regex101.com)。

## <a name="step-2-3-render-a-view-using-html"></a>步骤 2-3：使用 HTML 呈现视图

到目前为止，你在 views.py 中所拥有的 `index` 函数只会针对页面生成一个纯文本 HTTP 响应  。 当然，大多数实际 Web 页面都使用丰富的 HTML 页面进行响应，这些页面通常包含实时数据。 实际上，使用函数定义视图的主要原因是让你能够通过动态方式生成该内容。

`HttpResponse` 的参数只是一个字符串，因此可以在一个字符串中随意生成任何 HTML。 举一个简单的例子，用下面的代码替换 `index` 函数（保留现有 `from` 语句），这将使用动态内容生成 HTML 响应，每次刷新页面时都会更新：

```python
from datetime import datetime

def index(request):
    now = datetime.now()

    html_content = "<html><head><title>Hello, Django</title></head><body>"
    html_content += "<strong>Hello Django!</strong> on " + now.strftime("%A, %d %B, %Y at %X")
    html_content += "</body></html>"

    return HttpResponse(html_content)
```

再次运行该项目并看到类似于“Hello Django!  2018 年 4 月 16 日(星期一) 16:28:10”的消息。 刷新页面以更新时间并确认通过每个请求生成了内容。 完成后，请停止服务器。

> [!Tip]
> 要停止并重启项目，其快捷方式是使用“调试” > “重启”菜单命令 (Ctrl+Shift+F5)，或者使用调试工具栏上的“重启”按钮       ：
>
> ![Visual Studio 中调试工具栏上的重启按钮](media/debugging-restart-toolbar-button.png)

## <a name="step-2-4-render-a-view-using-a-page-template"></a>步骤 2-4：使用页面模板呈现视图

在代码中生成 HTML 适用于非常小的页面，但是随着页面变得越来越复杂，通常需要保留页面的静态 HTML 部分（以及对 CSS 和 JavaScript 文件的引用）作为“页面模板”，然后在其中插入代码生成的动态内容。 在上一节中，只有来自 `now.strftime` 调用的日期和时间是动态的，这意味着所有其他内容都可以放置在页面模板中。

Django 页面模板是一个 HTML 块，它可以包含称为“变量”的任何数量的替换标记，由 `{{` 和 `}}` 进行分隔，如 `{{ content }}` 中所示。 Django 的模板模块随后使用你在代码中提供的动态内容替换变量。

下面的步骤演示了如何使用页面模板：

1. 在包含的 Django 项目的 BasicProject 文件夹下，打开 settings.py 文件，并将应用名称“HelloDjangoApp”添加到 `INSTALLED_APPS` 列表   。 将应用添加到列表，告知 Django 项目有一个采用该名称，且包含一个应用的文件夹：

    ```python
    INSTALLED_APPS = [
        'HelloDjangoApp',
        # Other entries...
    ]
    ```

1. 另外，在 settings.py 中，确保 `TEMPLATES` 对象包含以下行（默认情况下包含），以指示 Django 在已安装应用的 templates 文件夹中查找模板   ：

    ```json
    'APP_DIRS': True,
    ```

1. 在 HelloDjangoApp 文件夹中，打开 templates/HelloDjangoApp/index.html 页面模板文件（在 VS 2017 15.7 及更早版本中，则为 templates/index.html），查看其是否包含一个变量 `{{ content }}`    ：

    ```html
    <html>
    <head><title></title></head>

    <body>

    {{ content }}

    </body>
    </html>
    ```

1. 在 HelloDjangoApp 文件夹中，打开 views.py 并将 `index` 函数替换为以下使用 `django.shortcuts.render` 帮助程序函数的代码   。 `render` 帮助程序为使用页面模板提供了一个简化的界面。 请务必保留所有现有 `from` 语句。

    ```python
    from django.shortcuts import render   # Added for this step

    def index(request):
        now = datetime.now()

        return render(
            request,
            "HelloDjangoApp/index.html",  # Relative path from the 'templates' folder to the template file
            # "index.html", # Use this code for VS 2017 15.7 and earlier
            {
                'content': "<strong>Hello Django!</strong> on " + now.strftime("%A, %d %B, %Y at %X")
            }
        )
    ```

    如你所见，`render` 的第一个参数是后跟应用的 templates 文件夹中模板文件相对路径的请求对象  。 在适当情况下，将为视图支持的模板文件命名。 `render` 的第三个参数则是模板引用的变量字典。 可以在字典中包含对象，在这种情况下，模板中的变量可以引用 `{{ object.property }}`。

1. 运行项目并观察输出。 应会看到与步骤 2-2 中所示类似的消息，它表示模板可正常使用。

    但是，请注意，在 `content` 属性中使用的 HTML 只呈现为纯文本，因为 `render` 函数会自动转义该 HTML。 自动转义防止意外漏洞注入攻击：开发人员通常从一页收集输入并通过模板占位符将其用作另一页的值。 转义还充当提醒：最好将 HTML 放置在页面模板中以及代码外。 还好，在需要时创建其他变量比较简单。 例如，通过“模板”更改 index.html，使其匹配下列标记，这会添加一个页标题并在页面模板中保留所有格式   ：

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
        </head>
        <body>
            <strong>{{ message }}</strong>{{ content }}
        </body>
    </html>
    ```

    然后按照下面的方式编写 `index` 视图函数，为页面模板中的所有变量提供值：

    ```python
    def index(request):
        now = datetime.now()

        return render(
            request,
            "HelloDjangoApp/index.html",  # Relative path from the 'templates' folder to the template file
            # "index.html", # Use this code for VS 2017 15.7 and earlier
            {
                'title' : "Hello Django",
                'message' : "Hello Django!",
                'content' : " on " + now.strftime("%A, %d %B, %Y at %X")
            }
        )
    ```

1. 停止服务器并重新启动项目，然后观察页面现在是否正确呈现：

    ![使用模板运行应用](media/django/step02-result.png)

1. <a name="template-namespacing"></a>Visual Studio 2017 版本 15.7 及更高版本：作为最后一步，将模板移动到与应用名称相同的子文件夹中，这样就可以创建一个命名空间，并避免与可能添加到项目中的其他应用发生潜在冲突。 （VS 2017 15.8 及更高版本中的模板会自动执行此操作。）即，在 templates 中创建名为 HelloDjangoApp 的子文件夹，将 index.html 移动到该子文件夹，并修改 `index` 查看函数以引用模板的新路径 HelloDjangoApp/index.html     。 然后运行项目，验证页面是否正确呈现，并停止服务器。

1. 如果需要，将更改提交到源代码管理并更新远程存储库，如[步骤 2-2](#commit-to-source-control) 中所述。

### <a name="question-do-page-templates-have-to-be-in-a-separate-file"></a>问：页面模板必须在一个单独的文件中吗？

答：尽管模板通常会保留在单独的 HTML 文件中，但也可以使用内联模板。 但是，建议使用单独的文件使标记和代码完全分离。

### <a name="question-must-templates-use-the-html-file-extension"></a>问：模板必须使用 .html 文件扩展名吗？

答：页面模板文件的 .html 扩展名是完全可选的，因为你始终可以识别出 `render` 函数第二个参数中文件的确切相对路径  。 然而，Visual Studio（和其他编辑器）通常会在 .html 文件中提供代码完成和语法着色等功能，这比页面模板不是严格的 HTML 更重要  。

实际上，在使用 Django 项目时，Visual Studio 会自动检测到你正在编辑的 HTML 文件实际上是 Django 模板，并提供某些自动完成功能。 例如，在开始键入 Django 页面模板注释 `{#` 时，Visual Studio 会自动提供右边的 `#}` 字符。 “注释选定内容”  和“取消注释选定内容”  命令（在“编辑”   > “高级”  菜单上和工具栏上）也使用模板注释，而不是 HTML 注释。

### <a name="question-when-i-run-the-project-i-see-an-error-that-the-template-cannot-be-found-whats-wrong"></a>问：运行项目时发生了一个错误：找不到模板。 为什么会这样？

答：如果看到无法找到模板的错误，请确保已将应用添加到 Django 项目 `INSTALLED_APPS` 列表的 settings.py 中  。 如果没有该条目，Django 将不知道在应用的 templates 文件夹中查找  。

### <a name="question-why-is-template-namespacing-important"></a>问：为什么模板命名空间如此重要？

答：当 Django 查找 `render` 函数中引用的模板时，它会使用第一次找到的与相对路径匹配的任何文件。 如果在同一个项目中有多个使用模板相同文件夹结构的 Django 应用，很可能会有一个应用无意中使用来自另一个应用的模板。 要避免此类错误，请始终在应用的 templates 文件夹下创建一个子文件夹，该文件夹与应用名称相匹配，可以避免任何重复  。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [为静态文件提供服务、添加页面和使用模板继承](learn-django-in-visual-studio-step-03-serve-static-files-and-add-pages.md)

## <a name="go-deeper"></a>深入了解

- [编写你的第一个 Django 应用，第 1 部分 - 视图](https://docs.djangoproject.com/en/2.0/intro/tutorial01/#write-your-first-view) (docs.djangoproject.com)
- 有关 Django 模板的更多功能（如包含和继承），请参阅 [Django 模板语言](https://docs.djangoproject.com/en/2.0/ref/templates/language/) (docs.djangoproject.com)
- [inLearning 上的正则表达式培训](https://www.linkedin.com/learning/topics/regular-expressions) (LinkedIn)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
