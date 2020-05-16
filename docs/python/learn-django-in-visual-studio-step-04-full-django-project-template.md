---
title: 学习 Visual Studio 中的 Django 教程的第 4 步，Web 项目模板
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了 Django Web 项目模板提供的功能。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: c778d830b20797962306700a5af938eb3a3bb142
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "62961668"
---
# <a name="step-4-use-the-full-django-web-project-template"></a>步骤 4：使用完整的 Django Web 项目模板

上一步：[为静态文件提供服务、添加页面和使用模板继承](learn-django-in-visual-studio-step-03-serve-static-files-and-add-pages.md) 

通过在 Visual Studio 中的“空白 Django Web 项目”模板上生成应用，你已经了解了 Django 的基础知识，现在可以轻松地了解“Django Web 项目”模板生成的更完整的应用。

在此步骤中，将执行以下操作：

> [!div class="checklist"]
> - 使用“Django Web 项目”模板创建一个更完整的 Django Web 应用并检查项目结构（步骤 4-1）
> - 了解由项目模板创建的视图和页面模板，该模板由三个继承自基本页面模板的页面组成，并使用 jQuery 和 Bootstrap 等静态 JavaScript 库（步骤 4-2）
> - 了解模板提供的 URL 路由（步骤 4-3）

该模板还提供基本身份验证，详情请参见步骤 5。

## <a name="step-4-1-create-a-project-from-the-template"></a>步骤 4-1：通过模板创建项目

1. 在 Visual Studio 中，转到解决方案资源管理器，右键单击在本教程前面创建的“LearningDjango”解决方案，并选择“添加” > “新项目”     。 （或者，如果想要使用新的解决方案，请改为选择“文件”   > “新建”   > “项目”  。）

1. 在“新建项目”对话框中，搜索并选择“Django Web 项目”模板，调用项目“DjangoWeb”并选择“确定”   。

1. 因为模板再次包含 requirements.txt 文件，Visual Studio 会询问在何处安装这些依赖项  。 选择“安装到虚拟环境”  选项，然后在“添加虚拟环境”  对话框中，选择“创建”  以接受默认设置。

1. 在 Visual Studio 完成设置虚拟环境后，按照 readme.html 中显示的说明创建 Django 超级用户（即管理员）  。 只需右键单击 Visual Studio 项目并选择“Python”   > “Django 创建超级用户”  命令，然后按照提示进行操作。 请务必记录你的用户名和密码，因为在执行应用的身份验证功能时会用到。

1. 若要将“DjangoWeb”项目设置为 Visual Studio 解决方案的默认值，可以在解决方案资源管理器中右键单击该项目，然后选择“设为启动项目”    。 启动项目（以粗体显示）会在启动调试器时运行。

    ![将 DjangoWeb 项目显示为启动项目的解决方案资源管理器](media/django/step04-second-project-in-solution-set-as-startup-project.png)

1. 选择“调试” > “启动调试”(F5) 或使用工具栏上的“Web 服务器”按钮运行服务器     ：

    ![Visual Studio 中的运行 Web 服务器工具栏按钮](media/django/run-web-server-toolbar-button.png)

1. 该模板创建的应用有三个页面：“主页”、“关于”和“联系信息”，可以使用导航栏在其中进行导航。 花一到两分钟的时间检查应用的不同部分。 若要通过“登录”  命令对应用进行身份验证，请使用前面创建的超级用户凭据。

    ![Django Web 项目应用的完整浏览器视图](media/django/step04-full-app-desktop-view.png)

1. 由“Django Web 项目”模板创建的应用将引导用于响应式布局，以适应移动设备外形规格。 要查看此响应能力，可以将浏览器调整为窄视图，使内容垂直显示，并使导航栏变为菜单图标：

    ![Django Web 项目应用的移动（窄）视图](media/django/step04-full-app-mobile-view.png)

1. 可以在以下各节中使应用保持运行状态。

    若要停止应用并[将更改提交到源代码管理](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)，首先打开团队资源管理器中的“更改”页，右键单击虚拟环境的文件夹（可能是 env），然后选择“忽略这些本地项”     。

### <a name="examine-what-the-template-creates"></a>检查模板创建的内容

在最广泛的层面上，“Django Web 项目”模板创建以下结构：

- 项目根目录中的文件：
  - manage.py，Django 管理实用工具  。
  - db.sqlite3，默认 SQLite 数据库  。
  - requirements.txt 包含了 Django 1.x 上的依赖项  。
  - readme.html，此文件在创建项目后显示在 Visual Studio 中  。 如上一节所述，请按照此处的说明为应用创建一个超级用户（管理员）帐户。
- app 文件夹包含所有应用文件，包括视图、模型、测试、窗体、模板和静态文件（请参阅步骤 4-2）  。 通常会重命名此文件夹，使用一个更有特色的应用名称。
- DjangoWeb （Django 项目）文件夹包含典型的 Django 项目文件：\_\_init\_\_.py、settings.py、urls.py 和 wsgi.py      。 通过使用项目模板，已经为应用和数据库文件配置了 settings.py，且为 urls.py 配置了到所有应用程序页（包括登录窗体）的路由   。

### <a name="question-is-it-possible-to-share-a-virtual-environment-between-visual-studio-projects"></a>问：能否能在 Visual Studio 项目之间共享虚拟环境？

答：可以，但在执行此操作时请注意，随着时间的推移，不同的项目可能会使用不同的包，因此共享的虚拟环境必须包含使用它的所有项目的所有包。

不过，若要使用现有的虚拟环境，需执行以下操作：

1. 当系统提示在 Visual Studio 中安装依赖项时，请选择“我将自行安装”  选项。
1. 在“解决方案资源管理器”  中，右键单击“Python 环境”  节点并选择“添加现有虚拟环境”  。
1. 导航到包含虚拟环境的文件夹并选中它，然后选择“确定”  。

## <a name="step-4-2-understand-the-views-and-page-templates-created-by-the-project-template"></a>步骤 4-2：了解通过项目模板创建的视图和页面模板

正如你在运行项目时所观察到的，该应用包含三个视图：“主页”、“关于”和“联系信息”。 这些视图的代码位于 app/views 文件夹中  。 每个视图函数都只是调用 `django.shortcuts.render`，其中包含通往模板和简单字典对象的路径。 例如，“关于”页面由 `about` 函数来处理：

```python
def about(request):
    """Renders the about page."""
    assert isinstance(request, HttpRequest)
    return render(
        request,
        'app/about.html',
        {
            'title':'About',
            'message':'Your application description page.',
            'year':datetime.now().year,
        }
    )
```

模板位于应用的 templates/app 文件夹中（通常希望将 app 重命名为实际应用名称）   。 基本模板 layout.html 的使用最为广泛  。 它指的是所有必需的静态文件（JavaScript 和 CSS），定义了其他页面覆盖的名为“内容”的块，并提供了另一个名为“脚本”的块。 以下来自 layout.html 的注释的摘录内容显示了这些特定区域  ：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <!-- Define a viewport for Bootstrap's responsive rendering -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title }} - My Django Application</title>

    {% load staticfiles %}
    <link rel="stylesheet" type="text/css" href="{% static 'app/content/bootstrap.min.css' %}" />
    <link rel="stylesheet" type="text/css" href="{% static 'app/content/site.css' %}" />
    <script src="{% static 'app/scripts/modernizr-2.6.2.js' %}"></script>
</head>
<body>
    <!-- Navbar omitted -->

    <div class="container body-content">

<!-- "content" block that pages are expected to override -->
{% block content %}{% endblock %}
        <hr/>
        <footer>
            <p>&copy; {{ year }} - My Django Application</p>
        </footer>
    </div>

<!-- Additional scripts; use the "scripts" block to add page-specific scripts.  -->
    <script src="{% static 'app/scripts/jquery-1.10.2.js' %}"></script>
    <script src="{% static 'app/scripts/bootstrap.js' %}"></script>
    <script src="{% static 'app/scripts/respond.js' %}"></script>
{% block scripts %}{% endblock %}

</body>
</html>
```

每个单页模板 about.html、contact.html、index.html 均扩展了基本模板 layout.html     。 about.html 最简单，它显示 `{% extends %}` 和 `{% block content %}` 标记  ：

```html
{% extends "app/layout.html" %}

{% block content %}

<h2>{{ title }}.</h2>
<h3>{{ message }}</h3>

<p>Use this area to provide additional information.</p>

{% endblock %}
```

index.html 和 contact.html 使用相同的结构，在“内容”块中提供更长的内容   。

templates / app 文件夹中还具有第 4 页 login.html，以及使用 `{% include %}` 引入 layout.html 的 loginpartial.html     。 这些模板文件在有关身份验证的步骤 5 中进行了讨论。

### <a name="question-can--block--and--endblock--be-indented-in-the-django-page-template"></a>问：在 Django 页面模板中是否可以缩进 {% block %} 和 {% endblock %}？

答：可以，如果缩进块标记，Django 页面模板操作正常，也许可以将它们对齐到适当的父元素中。 它们不会在 Visual Studio 项目模板生成的页面模板中缩进，这样就可以清楚地看到它们所在的位置。

## <a name="step-4-3-understand-the-url-routing-created-by-the-template"></a>步骤 4-3：了解模板创建的 URL 路由

由“Django Web 项目”模板创建的 Django 项目的 urls.py 文件包含以下代码  ：

```python
from datetime import datetime
from django.conf.urls import url
import django.contrib.auth.views

import app.forms
import app.views

urlpatterns = [
    url(r'^$', app.views.home, name='home'),
    url(r'^contact$', app.views.contact, name='contact'),
    url(r'^about$', app.views.about, name='about'),
    url(r'^login/$',
        django.contrib.auth.views.login,
        {
            'template_name': 'app/login.html',
            'authentication_form': app.forms.BootstrapAuthenticationForm,
            'extra_context':
            {
                'title': 'Log in',
                'year': datetime.now().year,
            }
        },
        name='login'),
    url(r'^logout$',
        django.contrib.auth.views.logout,
        {
            'next_page': '/',
        },
        name='logout'),
]
```

前三个 URL 模式直接映射到应用 views.py 文件中的 `home`、`contact` 和 `about` 视图中  。 另一方面，模式 `^login/$` 和 `^logout$` 使用内置的 Django 视图，而不是应用定义的视图。 对 `url` 方法的调用还包含用于自定义视图的额外数据。 步骤 5 探讨了这些调用。

### <a name="question-in-the-project-i-created-why-does-the-about-url-pattern-uses-about-instead-of-about-as-shown-here"></a>问：在我创建的项目中，为什么“about”URL 模式使用此处所示的“^about”而不是“^about$”？

答：正则表达式中缺少尾随的“$”是许多版本的项目模板中的一个普遍疏忽。 URL 模式非常适用于名为“about”的页面，但如果没有尾随的“$”，URL 模式还会匹配诸如“about=django”、“about09876”、“aboutoflaughter”等 URL。 此处显示的尾随“$”用于创建 URL 模式，该模式只  匹配“about”。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Django 中对用户进行身份验证](learn-django-in-visual-studio-step-05-django-authentication.md)

## <a name="go-deeper"></a>深入了解

- [将 Web 应用部署到 Azure App Service](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [编写你的第一个 Django 应用，第 4 部分 - 窗体和通用视图](https://docs.djangoproject.com/en/2.0/intro/tutorial04/) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
