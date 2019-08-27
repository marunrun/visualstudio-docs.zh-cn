---
title: Python 的 Web 应用程序模板
description: Visual Studio 使用 Bottle、Flask 和 Django 框架为 Python Web 应用程序提供模板；支持包括调试配置和发布到 Azure 应用程序服务。
ms.date: 01/28/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 952c4d9ab82275ff7b1550a3704e89b93c6260a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62954794"
---
# <a name="python-web-application-project-templates"></a>Python Web 应用程序项目模板

Visual Studio 中的 Python 支持在 Bottle、Flask 和 Django 框架中通过项目模板和可配置为处理不同框架的调试启动程序开发 Web 项目。 这些模板包括 requirements.txt 文件来声明必需的依赖项。 基于其中一个模板创建项目时，Visual Studio 会提示安装这些包（请参阅本文后面的[安装项目要求](#install-project-requirements)）。

也可以使用其他框架（如 Pyramid）的通用“Web 项目”模板。 在这种情况下，不会随模板一起安装框架。 而是将必要的包安装到用于项目的环境中（请参阅 [Python 环境窗口 - 包选项卡](python-environments-window-tab-reference.md#packages-tab)）。

有关将 Python Web 应用部署到 Azure 的信息，请参阅[发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)。

## <a name="use-a-project-template"></a>使用项目模板

使用“文件” > “新建” > 项目”从模板中创建项目。 要查看 Web 项目的模板，请选择对话框左侧的“Python” > “Web”。 然后选择你所选的模板，提供项目和解决方案名称，设置解决方案目录和 Git 存储库选项，然后选择“确定”。

![Web 应用的“新建项目”对话框](media/projects-new-project-dialog-web.png)

前面提到的通用“Web 项目”模板只提供了一个空的 Visual Studio 项目，只有一个 Python 项目，没有代码，也没有任何假设。 有关“Azure 云服务”模板的详细信息，请参阅 [Python 的 Azure 云服务项目](python-azure-cloud-service-project-template.md)。

所有其他模板都基于 Bottle、Flask 或 Django Web 框架，可以分为如以下各节所述的三个通用组。 由其中任一模板创建的应用中的代码都足以在本地运行和调试应用。 每个模板还提供必要的 [WSGI 应用对象](https://www.python.org/dev/peps/pep-3333/) (python.org)，以用于生产 Web 服务器。

### <a name="blank-group"></a>空白组

所有“空白 \<框架> Web 项目”模板都会创建一个项目，其中包含极少的样本代码以及 requirements.txt 文件中声明的必要依赖项。

| 模板 | 说明 |
| --- | --- |
| **空白 Bottle Web 项目** | 在 app.py 中生成最小的应用，其中包括 `/` 的主页和 `/hello/<name>` 页，它使用非常短的内嵌页模板回显 `<name>`。 |
| **空白 Django Web 项目** | 使用核心 Django 网站结构生成 Django 项目，但没有 Django 应用。 有关详细信息，请参阅 [Django 模板](python-django-web-application-project-template.md)和[学习 Django 步骤 1](learn-django-in-visual-studio-step-01-project-and-solution.md)。 |
| **空白 Flask Web 项目** | 生成包含 `/` 的单个“Hello World!”页的最小应用。 本应用类似于[快速入门中的以下详细步骤的结果：使用 Visual Studio 创建第一个 Python Web 应用](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)。 另请参阅[学习 Flask 步骤 1](learn-flask-visual-studio-step-01-project-solution.md)。

### <a name="web-group"></a>Web 组

所有“\<框架> Web 项目”模板都会创建一个具有相同设计的初学者 Web 应用，而与所选的框架无关。 该应用包含“主页”、“关于”和“联系人”页面，以及使用 Bootstrap 的导航栏和响应式设计。 每个应用都被适当地配置为提供静态文件（CSS、JavaScript 和字体），并使用适合框架的页面模板机制。

| 模板 | 说明 |
| --- | --- |
| **Bottle Web 项目** | 生成一个应用，其静态文件包含在 static 文件夹中，并通过 app.py 中的代码进行处理。 单个页面的路由包含在 routes.py 中，views 文件夹包含页面模板。|
| **Django Web 项目** | 生成一个 Django 项目和一个 Django 应用，其中包含三个页面、身份验证支持和一个 SQLite 数据库（但没有数据模型）。 有关详细信息，请参阅 [Django 模板](python-django-web-application-project-template.md)和[学习 Django 步骤 4](learn-django-in-visual-studio-step-04-full-django-project-template.md)。 |
| **Flask Web 项目** | 生成一个应用，其静态文件包含在 static 文件夹中。 views.py 中的代码处理路由，页面模板使用 templates 文件夹中包含的 Jinja 引擎。 runserver.py 文件提供启动代码。 请参阅[学习 Flask 步骤 4](learn-flask-visual-studio-step-04-full-flask-project-template.md)。 |
| **Flask/Jade Web 项目** | 生成与使用“Flask Web 项目”模板生成的相同的应用，但使用 Jade 模板引擎的 Jade 扩展。 |

### <a name="polls-group"></a>投票组

“投票 \<框架> Web 项目”模板创建一个初学者 Web 应用，用户可以通过该应用对不同的投票问题进行投票。 每个应用都基于“Web”项目模板的结构生成，从而使用数据库来管理投票和用户响应。 这些应用包含相应的数据模型以及用于从 samples.json 文件加载投票的特殊应用页 (/seed)。

| 模板 | 说明 |
| --- | --- |
| **投票 Bottle Web 项目** | 生成可以针对使用 `REPOSITORY_NAME` 环境变量配置的内存中数据库、MongoDB 或 Azure 表存储运行的应用。 数据模型和数据存储代码包含在 models 文件夹中，settings.py 文件包含用于确定使用哪个数据存储的代码。 |
| **投票 Django Web 项目** | 生成一个 Django 项目和一个 Django 应用，其中包含三个页面和一个 SQLite 数据库。 加入对 Django 管理界面的自定义设置，以允许经过身份验证的管理员创建和管理投票。 有关详细信息，请参阅 [Django 模板](python-django-web-application-project-template.md)和[学习 Django 步骤 6](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md)。 |
| **投票 Flask Web 项目** | 生成可以针对使用 `REPOSITORY_NAME` 环境变量配置的内存中数据库、MongoDB 或 Azure 表存储运行的应用。 数据模型和数据存储代码包含在 models 文件夹中，settings.py 文件包含用于确定使用哪个数据存储的代码。 该应用对页面模板使用 Jinja 引擎。 请参阅[学习 Flask 步骤 5](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md)。 |
| **投票 Flask/Jade Web 项目** | 生成与使用“投票 Flask Web 项目”模板生成的相同的应用，但使用 Jade 模板引擎的 Jade 扩展。 |

## <a name="install-project-requirements"></a>安装项目要求

从特定于框架的模板创建项目时，会出现一个对话框，有助于使用 pip 安装所需的包。 我们还建议对 Web 项目使用[虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)，以便发布网站时包含正确的依赖关项：

![为项目模板安装所需包的对话框](media/template-web-requirements-txt-wizard.png)

如果使用的是源代码管理，通常会忽略虚拟环境文件夹，因为该环境只能使用 requirements.txt 重新创建。 排除文件夹的最佳方法是先在上面的提示中选择“我将自行安装”，然后在创建虚拟环境之前禁用自动提交。 有关详细信息，请参阅[学习 Django 教程 - 步骤 1-2 和 1-3](learn-django-in-visual-studio-step-01-project-and-solution.md#step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository) 以及[学习 Flask 教程 - 步骤 1-2 和 1-3](learn-flask-visual-studio-step-01-project-solution.md#step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository)。

部署到 Microsoft Azure App Service 时，选择一个 Python 版本作为[站点扩展](https://aka.ms/PythonOnAppService)并手动安装包。 此外，因为 Azure 应用服务从 Visual Studio 部署时不会自动安装 requirements.txt 文件中的包，请遵照 [aka.ms/PythonOnAppService](https://aka.ms/PythonOnAppService) 上的配置详细信息操作。

Microsoft Azure 云服务支持 requirements.txt 文件。 有关详细信息，请参阅 [Azure 云服务项目](python-azure-cloud-service-project-template.md)。

## <a name="debugging"></a>调试

启动 Web 项目进行调试时，Visual Studio 会在随机端口上启动一个本地 Web 服务器，并打开默认浏览器浏览至该地址和端口。 若要指定其他选项，请右键单击项目，选择“属性”和“Web 启动器”选项卡：

![常规 Web 模板的 Web 启动器属性](media/template-web-launcher-properties.png)

在“调试”组中：

- 搜索路径、脚本参数、解释器参数和解释器路径：这些选项与用于[普通调试](debugging-python-in-visual-studio.md)的相同。
- 启动 URL：指定要在浏览器中打开的 URL。 默认为 `localhost`。
- **端口号**：URL 中未指定端口时使用的端口（默认情况下，Visual Studio 会自动选择一个）。 此设置下，能够替代 `SERVER_PORT` 环境变量的默认值，该变量由模板用来配置本地调试服务器侦听的端口。

“Run Server 命令”和“Debug Server 命令”组（后者位于图像中所显示内容的下方）中的属性确定启动 Web 服务器的方式。 由于许多框架需要使用当前项目外的脚本，因此可在此处配置该脚本并将启动模块的名称作为参数进行传递。

- **命令**：可以是 Python 脚本（\*.py 文件）、模块名称（例如 `python.exe -m module_name`）或一行代码（例如 `python.exe -c "code"`）。 下拉列表中的值表明这些类型中有哪些适用。
- 参数：这些参数会在命令后的命令行上传递。
- **环境**：指定环境变量的 \<NAME>=\<VALUE> 对的新行分隔的列表。 这些变量在所有可能会修改环境的属性（例如端口号和搜索路径）后进行设定，因此可能会覆盖这些值。

任何项目属性或环境变量都可以使用 MSBuild 语法进行指定，例如：`$(StartupFile) --port $(SERVER_PORT)`。
`$(StartupFile)` 是启动文件的相对路径，`{StartupModule}` 是启动文件的可导入名称。 `$(SERVER_HOST)` 和 `$(SERVER_PORT)` 是普通的环境变量，由“启动 URL”和“端口号”属性自动设定或由“环境”属性设定。

> [!Note]
> “Run Server 命令”中的值通过“Debug” > “Start Server”命令或 Ctrl+F5 使用；“Debug Server 命令”组中的值通过“Debug” > “Start Debug Server”命令或 F5 使用。

### <a name="sample-bottle-configuration"></a>Bottle 示例配置

“Bottle Web 项目”模板包括执行必要配置的 Boilerplate 代码。 导入的 Bottle 应用可能不包含此代码，但在这种情况下，以下设置将使用已安装的 `bottle` 模块启动应用：

- **运行服务器命令**组：
  - **命令**：`bottle`（模块）
  - **参数**：`--bind=%SERVER_HOST%:%SERVER_PORT% {StartupModule}:app`

- **调试服务器命令**组：
  - **命令**：`bottle`（模块）
  - **参数**：`--debug --bind=%SERVER_HOST%:%SERVER_PORT% {StartupModule}:app`

使用 Visual Studio 进行调试时，不建议使用 `--reload` 选项。

### <a name="sample-pyramid-configuration"></a>Pyramid 示例配置

Pyramid 应用当前最好使用 `pcreate` 命令行工具进行创建。 创建应用后，可使用[“基于现有 Python 代码”](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files)模板将其导入。 这样操作后，选择“通用 Web 项目”自定义来配置选项。 这些设置假设将 Pyramid 安装到 `..\env` 处的虚拟环境。

- **调试**组：
  - **服务器端口**：6543（或 .ini 文件中配置的任何内容）

- **运行服务器命令**组：
  - 命令：`..\env\scripts\pserve-script.py`（脚本）
  - 参数：`Production.ini`

- **调试服务器命令**组：
  - 命令：`..\env\scripts\pserve-script.py`（脚本）
  - 参数：`Development.ini`

> [!Tip]
> 你可能需要配置项目的“工作目录”属性，因为 Pyramid 应用通常是项目根目录下的一个文件夹。

### <a name="other-configurations"></a>其他配置

如果有针对另一个要共享的框架的设置，或者要为另一个框架请求设置，则[在 GitHub 上提出问题](https://github.com/Microsoft/PTVS/issues)。

## <a name="convert-a-project-to-azure-cloud-service"></a>将项目转换为 Azure 云服务

“转换为 Microsoft Azure 云服务项目”命令（见下图）会将云服务项目添加到解决方案。 此项目包括要使用的虚拟机和服务的部署设置和配置。 使用云项目上的“发布”命令部署到云服务；Python 项目上的“发布”命令仍会部署到网站。 有关详细信息，请参阅 [Azure 云服务项目](python-azure-cloud-service-project-template.md)。

![“转换为 Microsoft Azure 云服务项目”命令](media/template-web-convert-menu.png)

## <a name="see-also"></a>请参阅

- [Python 项模板引用](python-item-templates.md)
- [发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)
