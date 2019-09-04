---
title: Python 的 Azure 云服务项目模板
description: Visual Studio 为使用 Python 编写的 Azure 云服务提供模板，包括角色部署、依赖项和故障排除。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 81dbe6189557f38daa23983a100c295654299a5d
ms.sourcegitcommit: 3cda0d58c5cf1985122b8977b33a171c7359f324
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154873"
---
# <a name="azure-cloud-service-projects-for-python"></a>Python 的 Azure 云服务项目

Visual Studio 提供的模板有助于使用 Python 创建 Azure 云服务。

[云服务](https://docs.microsoft.com/azure/cloud-services/)中包含数量不限的辅助角色和 Web 角色，其中每个角色执行在概念上独立的任务，但可根据缩放需求在虚拟机中单独复制   。 Web 角色为前端 Web 应用程序提供托管。 在使用 Python 的情况下，任何支持 WSGI 的 Web 框架都可用于编写这样的应用程序 - 如同受 [Web 项目模板](python-web-application-project-templates.md)支持一样。 辅助角色用于不直接与用户交互的长时间运行的进程。 它们通常使用同 [`pip install azure`](https://pypi.org/project/azure) 一起安装的“azure”包中的包。

本文详细介绍 Visual Studio 2017 及更高版本中的项目模板和其他支持（早期版本相似，但有一些差异）。 有关通过 Python 使用 Azure 的详细信息，请访问 [Azure Python 开发人员中心](https://docs.microsoft.com/azure/python/)。

## <a name="create-a-project"></a>创建项目

1. 安装需要使用云服务模板的[用于 Visual Studio 的 Azure.NET SDK](https://visualstudio.microsoft.com/vs/azure-tools/)。
1. 在 Visual Studio 中，选择“文件”   > “新建”   > “项目”  ，然后搜索“Azure Python”，并从列表中选择“Azure 云服务”  ：

    ![用于 Python 的 Azure 云项目模板](media/template-azure-cloud-project.png)

1. 选择要包括的一个或多个角色。 云项目可合并不同语言编写的角色，因此可轻松使用最适合的语言编写应用程序的各个部分。 若要在完成此对话框后向项目添加新角色，请右键单击“解决方案资源管理器”  中的“角色”  ，然后选择“添加”  下的某项。

    ![在 Azure 云项目模板中添加角色](media/template-azure-cloud-service-project-wizard.png)

1. 创建单个角色项目时，如果选择了使用其他 Python 软件包（如 Django、Bottle、Flask 框架）的角色，系统可能会提示安装该软件包。

1. 向项目添加新角色后，会出现配置说明。 配置更改通常不是必要的，但可能对以后自定义项目有用。 请注意，同时添加多个角色时，只有最后一个角色的说明保持打开状态。 但是，可以在其他角色的相应 readme.mht  文件中找到说明和故障排除提示，该文件位于角色的根目录或 bin  文件夹中。

1. 项目的 bin  文件夹还包含一个或两个用于配置远程虚拟机的 PowerShell 脚本，包括安装 Python、项目中任何 [requirements.txt  ](#dependencies) 文件和设置 IIS（如有需要）。 可以根据需要编辑这些文件以用于部署，也可以通过其他方式管理最常用选项（请参阅下面的[配置角色部署](#configure-role-deployment)）。 请勿删除这些文件，因为如果这些文件不可用，会改用旧版配置脚本。

    ![辅助角色支持文件](media/template-azure-cloud-service-worker-role-support-files.png)

    若要将这些配置脚本添加到新项目，请右键单击项目，选择“添加”   > “新建项目”  ，然后选择“Web 角色支持文件”  或“辅助角色支持文件”  。

## <a name="configure-role-deployment"></a>配置角色部署

角色项目的 bin  文件夹中的 PowerShell 脚本控制该角色的部署，并且可以编辑该脚本以自定义配置：

- ConfigureCloudService.ps1  适用于 Web 角色和辅助角色，通常用于安装和配置依赖项，以及设置 Python 版本。
- LaunchWorker.ps1  仅适用于辅助角色，可用于更改启动行为、添加命令行参数，或添加环境变量。

两个文件都包含自定义的说明。 此外，还可以通过向主要云服务项目的 ServiceDefinition.csdef  文件添加其他任务，以及将 `PYTHON` 变量设置为其已安装的 python.exe  （或等效的）路径这种方式，安装自己的 Python 版本。 如果设置 `PYTHON`，则不从 NuGet 安装 Python。

其他配置可通过如下操作完成：

1. 更新项目根目录中的 requirements.txt  文件后，使用 `pip` 来安装包。 ConfigureCloudService.ps1  脚本在部署时安装此文件。
1. 通过修改 web.config  文件（Web 角色）或 ServiceDefinition.csdef  文件（辅助角色）的 `Runtime` 部分，设置环境变量。
1. 通过修改 ServiceDefinitions.csdef  文件的 `Runtime/EntryPoint` 部分中的命令行，指定辅助角色要使用的脚本和参数。
1. 通过 web.config  文件设置 Web 角色的主要处理程序脚本。

## <a name="test-role-deployment"></a>测试角色部署

编写角色时，可以使用云服务仿真程序本地测试云项目。 仿真程序包含在 Azure SDK 工具中，是将云服务发布到 Azure 时使用的有限环境版本。

若要启动仿真程序，请先右键单击并选择“设为启动项目”  ，以确保解决方案中的云项目是启动项目。 然后选择“调试”   > “开始调试”  (F5  ) 或“调试”   > “启动而不调试”  (Ctrl  +F5  )。

请注意，由于仿真程序中的限制，不能调试 Python 代码。 因此，建议通过单独运行角色来进行调试，然后在发布前使用仿真程序进行集成测试。

## <a name="deploy-a-role"></a>部署角色

若要打开“发布”  向导，在“解决方案资源管理器”  中选择角色项目，然后从主菜单中选择“生成”   > “发布”  ，或者右键单击该项目，然后选择“发布”  。

发布过程包含两个阶段。 首先，Visual Studio 创建包含云服务的所有角色的单个包。 此包将部署到 Azure，为每个角色初始化一个或多个虚拟机，并部署源。

在每个虚拟机激活时，执行 ConfigureCloudService.ps1  脚本，并安装所有依赖项。 此脚本默认安装 [NuGet](https://www.nuget.org/packages?q=Tags%3A%22python%22+Authors%3A%22Python+Software+Foundation%22) 上最新版本的 Python，以及 requirements.txt  文件中指定的任何包。

最后，辅助角色执行 LaunchWorker.ps1  ，从而开始运行 Python 脚本；Web 角色初始化 IIS，并开始处理 Web 请求。

## <a name="dependencies"></a>依赖项

对于云服务，ConfigureCloudService.ps1  脚本使用 `pip` 安装一组 Python 依赖项。 应在名为 requirements.txt  的文件中指定依赖项（可通过修改 ConfigureCloudService.ps1  进行自定义）。 该文件通过 `pip install -r requirements.txt` 进行执行，作为初始化的一部分。

请注意，云服务实例不包括 C 编译器，因此，具有 C 扩展名的所有库都必须提供预编译二进制文件。

会自动下载 pip 及其依赖项，以及 requirements.txt  中的包，并且这些内容可能被计为付费的带宽使用。 有关管理 requirements.txt  文件的详细信息，请参阅[管理所需的包](managing-required-packages-with-requirements-txt.md)。

## <a name="troubleshooting"></a>疑难解答

如果部署后无法正常使用 Web 或辅助角色，请检查以下各项：

- Python 项目（至少）包含具有以下内容的 bin\\  文件夹：

  - *ConfigureCloudService.ps1*
  - *LaunchWorker.ps1*（仅适用于辅助角色）
  - *ps.cmd*

- Python 项目包含列出所有依赖项的 requirements.txt  （或滚轮文件的集合）。
- 在云服务上启用远程桌面，并调查日志文件。
- ConfigureCloudService.ps1  和 LaunchWorker.ps1  的日志存储在远程计算机的 C:\Resources\Directory\%RoleId%.DiagnosticStore\LogFiles  文件夹中。
- Web 角色可能将其他日志写入 web.config  配置的路径中，即 `WSGI_LOG` appSetting 中的路径。 最常规的 IIS 或 FastCGI 日志记录也会起作用。
- 目前，LaunchWorker.ps1.log  文件是查看 Python 辅助角色所显示的输出或错误的唯一方法。
