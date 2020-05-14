---
title: 适用于 Python 的 Django Web 项目模板
description: Visual Studio 为使用 Python 快速创建 Django web 应用程序提供了全面的模板。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 136c03ef11071e5d548e36e45a6a541cffce1469
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62784795"
---
# <a name="django-web-project-template"></a>Django Web 项目模板

[Django](https://www.djangoproject.com/) 是高级 Python 框架，用于快速、安全及可扩展的 Web 开发。 借助 Visual Studio 中的 Python 支持，可以使用多个项目模板来设置基于 Django 的 Web 应用程序的结构。 若要在 Visual Studio 中使用模板，请选择“文件” **“新建”** “项目”，搜索“Django”，然后从“空白 Django Web 项目”、“Django Web 项目”和“投票 Django Web 项目”模板中进行选择 >    >      。 有关所有模板的演练，请参阅 [Django 学习教程](learn-django-in-visual-studio-step-01-project-and-solution.md)。

Visual Studio 为 Django 项目提供完整的 IntelliSense：

- 传递给模板的上下文变量：

    ![IntelliSense 的上下文变量](media/template-django-intellisense.png)

- 针对内置和用户定义的标记和筛选器：

    ![IntelliSense 的标记和筛选器](media/template-django-intellisense-filter.png)

- 嵌入式 CSS 和 JavaScript 的语法着色：

    ![CSS IntelliSense](media/template-django-intellisense-css.png)

    ![JavaScript IntelliSense](media/template-django-intellisense-js.png)

Visual Studio 还为 Django 项目提供完整的[调试支持](debugging-python-in-visual-studio.md)：

![断点](media/template-django-debugging.png)

Django 项目一般通过其 manage.py 文件管理，Visual Studio 会遵循此假设  。 如果停止将该文件用作入口点，则实质上是中断了项目文件。 在这种情况下，需要[从现有文件重新创建项目](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files)，不将其标记为 Django 项目。

## <a name="django-management-console"></a>Django 管理控制台

Django 管理控制台可通过“项目”菜单上的各种命令或在解决方案资源管理器中右键单击项目进行访问   。

- **打开 Django Shell**：将打开应用程序上下文中的 shell，使你能够操作模型：

    ![“Open Django Shell”命令的结果](media/template-django-console-shell.png)

-  Django 同步数据库：在交互`manage.py syncdb`**窗口中执行** ：

    ![“Django Sync DB”命令的结果](media/template-django-console-sync-db.png)

- **收集静态文件**：执行 `manage.py collectstatic --noinput` 以将所有静态文件复制到由 settings.py 中的 `STATIC_ROOT` 指定的路径中  。

    ![“Collect Static”命令的结果](media/template-django-console-collect-static.png)

- **验证**：执行 `manage.py validate`，它将报告由 settings.py 中 `INSTALLED_APPS` 指定的已安装模型中的任何验证错误  ：

    ![“Validate”命令的结果](media/template-django-console-validate.png)

## <a name="see-also"></a>另请参阅

- [学习 Django 教程](learn-django-in-visual-studio-step-01-project-and-solution.md)
- [发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)
