---
title: 通过 Python 使用 CookieCutter 模板
description: Visual Studio 支持图形 Cookiecutter 扩展，以发现 Python 代码的模板并从这些模板创建项目。
ms.date: 01/28/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 026953ff52f4aa5c34dd4656432fed8ef2a48580
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535143"
---
# <a name="use-the-cookiecutter-extension"></a>使用 Cookiecutter 扩展

[Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) 可提供图形用户界面，用于发现模板、输入模板选项以及创建项目和文件。 Cookiecutter 随附在 Visual Studio 2017 及更高版本中，在 Visual Studio 早期版本中可单独安装。

Cookiecutter 需要 Python 3.3 或更高版本（32 位或 64 位）或者 Anaconda 3 4.2 或更高版本（32 位或 64 位）。 如果适用的 Python 解释器不可用，Visual Studio 将显示警告。 如果 Visual Studio 运行时安装 Python 解释器，请单击Cookiecutter 工具栏上的“主页”  按钮，检测新安装的解释器。 （请参阅 [Python 环境](managing-python-environments-in-visual-studio.md)了解有关整体环境的详细信息。）

安装后，选择“视图”   > “Cookiecutter 资源管理器”  打开其窗口：

![Cookiecutter 主窗口](media/cookiecutter-overview.png)

## <a name="cookiecutter-workflow"></a>Cookiecutter 工作流

如以下各节所述，使用 Cookiecutter 的过程为：浏览和选择模板、将其克隆到本地计算机、设置选项，然后基于该模板创建代码。

### <a name="browse-templates"></a>浏览模板

Cookiecutter 主页上显示可选择的模板列表，分为以下几组：

| 组 | 说明 |
| --- | --- |
| **已安装** | 已安装到本地计算机的模板。 使用联机模板时，其存储库自动克隆到 ~/.cookiecutters  的子文件夹。 可以通过按“删除”  ，删除所选的已安装模板。 |
| **建议** | 从建议源加载的模板。 默认源由 Microsoft 策划。 有关自定义源的详细信息，请参阅下文中的 [Cookiecutter 选项](#cookiecutter-options)。 |
| **GitHub** | GitHub cookiecutter 关键字的搜索结果。 分页显示从 GitHub 返回的结果，如果存在更多结果，列表末尾将出现**加载更多**。 |
| **自定义** | 如果在搜索框中输入自定义位置，该位置将出现在此组。 可键入到 GitHub 存储库的完整路径，或者到本地磁盘上的文件夹的完整路径。 |

### <a name="cloning"></a>克隆

选择模板，然后选择“下一步”  后，Cookiecutter 将生成待处理的本地副本。

如果选择“推荐”组或“GitHub”组中的模板，或在搜索框中输入自定义 URL 并选择该模板，模板会进行克隆并安装到本地计算机上   。 如果该模板已在 Visual Studio 的上一个会话中安装，将自动删除该模板，并且克隆最新版本。

如果从“已安装”组中选择模板或在搜索框中输入自定义文件夹路径并选择该模板，Visual Studio 将加载该模板，但不进行克隆  。

> [!Important]
> Cookiecutter 模板将克隆到单个文件夹 ~/.cookiecutters  下。 每个子文件夹将以 Git 存储库的名称命名（不包括 GitHub 用户名）。 如果克隆来作者不同但名称相同的模板，则可能会产生冲突。 在这种情况下，Cookiecutter 将阻止使用具有相同名称的其他模板覆盖现有模板。 若要安装其他模板，必须先删除现有模板。

### <a name="set-template-options"></a>设置模板选项

本地安装模板后，Cookiecutter 将显示选项页，在该页中可以指定 Cookiecutter 生成文件的位置以及其他选项：

![Cookiecutter 选项页](media/cookiecutter-template-options.png)

每个 Cookiecutter 模板定义各自的选项集，并为每个选项指定默认值（显示为每个条目字段中的建议文本）。 如果默认值是使用其他选项的动态值，则通常为代码片段。

使用用户配置文件可为特定选项自定义默认值。 Cookiecutter 扩展检测到用户配置文件时，会使用用户配置的默认值覆盖模板的默认值。 Cookiecutter 文档的[用户配置](https://cookiecutter.readthedocs.io/en/latest/advanced/user_config.html)部分对此行为进行了讨论。

如果模板指定在代码生成后运行特定的 Visual Studio 任务，则将显示附加的“完成后运行其他任务”  选项，该选项允许退出运行那些任务。 最常见的任务是打开 Web 浏览器、在编辑器中打开文件、安装依赖项等。

### <a name="create"></a>创建

设置选项后，请选择“创建”来生成代码（如果输出文件夹不为空，则会出现警告）  。 如果你对模板的输出很熟悉并且不介意覆盖文件，可以忽略该警告。 否则，请选择“取消”  ，指定一个空文件夹，然后将创建的文件手动复制到非空的输出文件夹。

成功创建文件后，Cookiecutter 提供在“解决方案资源管理器”  中打开文件的选项：

![显示解决方案资源管理器命令的 Cookiecutter](media/cookiecutter-files-created.png)

## <a name="cookiecutter-options"></a>Cookiecutter 选项

通过“工具”   > “选项”   > “Cookiecutter”  ，可使用 Cookiecutter 选项：

![Cookiecutter 选项](media/cookiecutter-tools-options.png)

| 选项 | 说明 |
| --- | --- |
| **建议的源 URL** | 建议模板源的位置。 它可以是本地文件的 URL 或路径。 将 URL 留空以使用默认的 Microsoft 策划的源。 源提供了由换行符分隔的模板位置的简单列表。 若要请求更改策划的源，请对 [GitHub 上的源](https://github.com/Microsoft/PTVS/blob/master/Python/Product/Cookiecutter/CookiecutterFeed.txt)拉取请求。 |
| **显示帮助** | 控制 Cookiecutter 窗口顶部的帮助信息栏的可见性。 |

## <a name="optimize-cookiecutter-templates-for-visual-studio"></a>优化用于 Visual Studio 的 Cookiecutter 模板

有关创作 Cookiecutter 模板的基础知识，请参阅 [Cookiecutter 文档](https://cookiecutter.readthedocs.io/en/latest/first_steps.html)。 用于 Visual Studio 的 Cookiecutter 扩展支持创建用于 Cookiecutter v1.4 的模板。

模板变量的默认呈现取决于数据类型（字符串或列表）：

- 字符串：变量名称的标签、输入值的文本框和显示默认值的水印。 文本框上的工具提示显示默认值。
- 列表：变量名称的标签、选择值的组合框。 组合框上的工具提示显示默认值。

通过在特定于 Visual Studio 的 cookiecutter.json  文件（并且 Cookiecutter CLI 忽略了该文件）中指定其他元数据，可以改进此呈现。 所有属性都是可选的：

| Property | 说明 |
| --- | --- |
| 标签 | 指定编辑器上方显示的关于变量的内容，而不是变量名称。 |
| 说明 | 指定编辑控件上显示的工具提示，而不是该变量的默认值。 |
| URL | 将标签转换为超链接，并使用工具提示显示该 URL。 单击超链接将打开用户默认浏览器，并转到该 URL。 |
| 选择器 | 允许为变量自定义编辑器。 目前支持以下选择器：<ul><li>`string`：标准文本框，默认用于符串。</li><li>`list`：标准组合框，默认用于列表。</li><li>`yesno`：在 `y` 和 `n` 之间进行选择的组合框，用于字符串。</li><li>`odbcConnection`：具有“...”  按钮的文本框，可用于打开数据库连接对话框。</li></ul> |

例如：

```json
{
    "site_name": "web-app",
    "python_version": ["3.5.2", "2.7.12"],
    "use_azure": "y",

    "_visual_studio": {
        "site_name": {
            "label": "Site name",
            "description": "E.g. <site-name>.azurewebsites.net (can only contain alphanumeric characters and `-`)"
        },
        "python_version": {
            "label": "Python version",
            "description": "The version of Python to run the site on"
        },
        "use_azure" : {
            "label": "Use Azure",
            "description": "Include Azure deployment files",
            "selector": "yesno",
            "url": "https://azure.microsoft.com"
        }
    }
}
```

### <a name="run-visual-studio-tasks"></a>运行 Visual Studio 任务

Cookiecutter 具有名为“后生成挂钩”的功能  ，允许文件生成后，运行任意 Python 代码。 此功能虽然灵活，但不允许方便地访问 Visual Studio。

例如，你可能想要在 Visual Studio 编辑器中，或在其 Web 浏览器中打开文件，或者触发用于提示用户创建虚拟环境并安装包要求的 Visual Studio UI。

为了实现这些需求，用户在“解决方案资源管理器”中打开生成文件后，或文件添加到现有项目后，Visual Studio 将在描述要运行的命令的 cookiecutter.json 中查找扩展元数据。 （同样，用户可以通过清除模板选项中的“完成后运行其他任务”，选择退出运行这些任务  。）

例如：

```json
"_visual_studio_post_cmds": [
    {
        "name": "File.OpenFile",
        "args": "{{cookiecutter._output_folder_path}}\\readme.txt"
    },
    {
        "name": "Cookiecutter.ExternalWebBrowser",
        "args": "https://docs.microsoft.com"
    },
    {
        "name": "Python.InstallProjectRequirements",
        "args": "{{cookiecutter._output_folder_path}}\\dev-requirements.txt"
    }
]
```

命令按名称指定并且应该使用未本地化的（英语）名称处理 Visual Studio 的本地化安装。 可以在 Visual Studio 命令  窗口中测试和发现命令名称。

如果要传递单个参数，请按照上述示例将其指定为字符串。

如果不需要传递参数，请将其保留为空字符串或在 JSON 中省略：

```json
"_visual_studio_post_cmds": [
    {
        "name": "View.WebBrowser"
    }
]
```

对于多个参数，请使用数组。 对于开关，请将开关及其值拆分为单独的参数并使用正确的引用。 例如:

```json
"_visual_studio_post_cmds": [
    {
        "name": "File.OpenFile",
        "args": [
            "{{cookiecutter._output_folder_path}}\\read me.txt",
            "/e:",
            "Source Code (text) Editor"
        ]
    }
]
```

参数可以引用其他 Cookiecutter 变量。 在上述示例中，内部的 `_output_folder_path` 变量用于生成该生成文件的绝对路径。

请注意，只有将文件添加到现有项目时，`Python.InstallProjectRequirements` 命令才有效。 存在此限制的原因是，该命令由 Python 项目在“解决方案资源管理器”  中处理，并且“解决方案资源管理器”   - “文件夹”  视图中没有用于接收的消息的项目。 我们希望在将来版本中消除此限制（并在总体上提供优化的文件夹视图  ）。

## <a name="troubleshooting"></a>故障排除

### <a name="error-loading-template"></a>加载模板时出错

某些模板可能正在其 cookiecutter.json  中使用无效的数据类型，如布尔值。 选择模板信息窗格中的“问题”链接即可向模板作者报告此类实例  。

### <a name="hook-script-failed"></a>挂钩脚本失败

某些模板可能使用与 Cookiecutter UI 不兼容的后期生成脚本。 例如，由于没有终端控制台，查询用户输入的脚本将失败。

### <a name="hook-script-not-supported-on-windows"></a>Windows 不支持挂钩脚本

如果后期脚本为 .sh  ，则可能与 Windows 计算机上的应用程序无关。 可能会出现一个 Windows 对话框，要求在 Windows 应用商店中查找兼容的应用程序。

### <a name="templates-with-known-issues"></a>具有已知问题的模板

克隆失败：

- **wildfish/cookiecutter-django crud**（子文件夹名称中的无效字符 `|`）
- **cookiecutter-pyvanguard**（子文件夹名称中的无效字符 `|`）

加载失败：

- chrisdev/wagtail-cookiecutter-foundation  （在 cookiecutter.json  中使用布尔值类型）
- **quintoandar/cookiecutter android**（无模板文件夹）

运行失败：

- **iknite/cookiecutter-ansible-role**（后期挂钩脚本需要控制台输入）
- **benregn/cookiecutter-django ansible**（jinja 错误）

使用 Bash（非致命）：

- **openstack-dev/cookiecutter**
