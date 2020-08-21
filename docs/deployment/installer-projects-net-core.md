---
title: Visual Studio 安装程序项目和 .NET Core 3。1
ms.date: 08/18/2020
ms.topic: conceptual
helpviewer_keywords:
- installer projects
- installer projects, .NETCore
author: MSLukeWest
ms.author: lukewest
manager: MSLukeWest
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: c35e6a12262083d09575b51f6c9f918ba30a27b1
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714383"
---
# <a name="visual-studio-installer-projects-extension-and-net-core-31"></a>Visual Studio 安装程序项目扩展和 .NET Core 3。1

通常使用 Visual Studio 安装程序项目扩展将应用程序打包为 MSI。

可在此处下载扩展： [Visual Studio 安装程序项目](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)

## <a name="update-for-net-core"></a>.NET Core 更新
.NET Core 有两种不同的模型用于发布。

- 依赖框架的部署

- 自包含应用程序包括运行时。

若要了解有关这些部署策略的详细信息，请参阅 [.Net Core 应用程序发布概述](https://docs.microsoft.com/dotnet/core/deploying/)。

### <a name="workflow-changes-for-net-core-31"></a>.NET Core 3.1 的工作流更改

1. 选择 " **发布项** 而不是 **主输出** "，以获取 .net Core 3.1 项目的正确输出。  若要打开此对话框，请**Add**  >  从项目的上下文菜单中选择 "添加**项目输出 ...** "。

    !["添加项目输出组" 对话框中的 "发布项" 输出组](../deployment/media/installer-projects-net-core-publish-items-output.png "选择发布项")

2. 若要创建独立的安装程序，请在安装项目的 "**发布项**" 节点上设置**PublishProfilePath**属性，并使用具有正确属性集的发布配置文件的相对路径。

    ![在 "发布项" 项目输出项中设置发布配置文件](../deployment/media/installer-projects-net-core-publish-profile.png "设置发布配置文件")

### <a name="prerequisites-for-net-core-31"></a>.NET Core 3.1 的先决条件

如果希望安装程序能够为依赖于框架的 .NET Core 3.1 应用安装所需的运行时，则可以使用 [先决条件](../deployment/application-deployment-prerequisites.md)执行此操作。  从安装程序项目的 "属性" 对话框中，打开 " **先决条件 ...** " 对话框，你将看到以下条目：

!["必备组件" 对话框中的 .NET Core 项](../deployment/media/installer-projects-net-core-prerequisites.png ".NET Core 系统必备组件")

应为控制台应用程序选择 " **.Net Core 运行时** ..." 选项，并为 WPF/WinForms 应用程序选择 " **.Net 桌面运行时 ...** "。

>[!NOTE]
>Visual Studio 2019 Update 7 版本中提供了这些项。

## <a name="see-also"></a>另请参阅

- [“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)
- [应用程序部署先决条件](../deployment/application-deployment-prerequisites.md)
