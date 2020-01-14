---
title: 如何：将扩展性项目迁移到 Visual Studio 2015 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, upgrading
ms.assetid: 22491cdc-8f04-4e1c-8eb4-ff33798ec792
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e2f4926a503304491164635b983353ba7f3bb0f6
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75915973"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2015"></a>如何：将扩展性项目迁移到 Visual Studio 2015
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下面介绍了如何升级扩展。  
  
> [!IMPORTANT]
> 如果要为 Visual Studio 的早期版本维护扩展解决方案的版本，请确保在升级之前进行复制。 可能很难将升级后的版本恢复到以前的状态。  
  
#### <a name="to-upgrade-an-extensibility-solution"></a>升级扩展性解决方案  
  
1. 使用要升级的副本，在新版本中打开它。 建议升级不可逆。  
  
2. 升级完成后，将外部程序的路径更改为新版本的 node.js。 右键单击 "**解决方案资源管理器**中的项目节点，然后选择"**属性**"。 在 "**调试**" 选项卡中，通过 "**启动外部程序**" 查找文本框，并将 devenv 的路径更改为 Visual Studio 2015 路径，如下所示：  
  
     **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe**  
  
3. 添加一个对 VisualStudio 的引用。 （右键单击 "**解决方案资源管理器**中的项目节点，然后选择"**添加/引用**"。 选择 "**扩展**" 选项卡，然后检查**VisualStudio**。）  
  
4. 生成解决方案。 生成的文件部署到：  
  
     **%LOCALAPPDATA%\Microsoft\VisualStudio.14.0Exp\Extensions\\< 作者名称\>\\< 项目名称**\>\\\>项目版本 \\。  
  
#### <a name="to-update-an-extensibility-project-to-nuget-vs-sdk-reference-assemblies"></a>将扩展性项目更新为 NuGet VS SDK 引用程序集  
  
1. 确定你的项目所需的 VS SDK 引用程序集。  在**解决方案资源管理器**中，展开项目的 "**引用**" 节点，并查看项目引用的列表。  VS SDK 引用程序集将在名称中包含前缀**VisualStudio** （例如： VisualStudio）。  
  
2. 通过选择该程序集，然后右键单击并**删除**，从项目中删除 VS SDK 引用程序集。  
  
3. 添加 VS SDK 引用程序集的 NuGet 版本。  仍在 "**解决方案资源管理器引用**" 节点中，打开 "**管理 NuGet 包 ...** " 对话框中的字段。  如果要了解有关此对话框的详细信息，请参阅[使用对话框管理 NuGet 包](/nuget/consume-packages/install-use-packages-visual-studio)。 VS SDK 引用程序集通过[VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility)发布在[nuget.org](https://www.nuget.org/)上。  
  
4. 使用**nuget.org**作为**包源**，搜索与所需的引用程序集匹配的 nuget 包名称（例如： VisualStudio），并将其安装在你的项目中。  NuGet 可能会添加多个引用程序集，以便满足初始程序集的依赖关系。  
  
     如果愿意，可以通过安装 VS SDK[元包](https://www.nuget.org/packages/VSSDK_Reference_Assemblies)一次添加所有 vs sdk 引用程序集。  
  
5. 还可以切换到使用 NuGet 版本的 VS SDK 生成工具。 此 NuGet 包是[VSSDK](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools) ，添加到你的项目后，将包括必要的工具和目标文件，使你能够在未安装 VS SDK 的计算机上生成扩展性项目。  
  
> [!NOTE]
> 不要求您更新现有的扩展性项目以使用 NuGet 引用程序集和工具。  他们可以继续使用与 VS SDK 一起安装的引用程序集和工具进行构建。
