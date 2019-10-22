---
title: 多定向概述 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- targeting .NET Framework version [Visual Studio]
- versions [Visual Studio], targeting .NET Framework version
- multi-targeting [Visual Studio]
- multitargeting [Visual Studio]
ms.assetid: b1702c33-0672-4ebc-b779-2b324d6ea880
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba7566e4a6bdffc5e7075bc138832097415a7129
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667098"
---
# <a name="visual-studio-multi-targeting-overview"></a>Visual Studio 多目标概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在此版本的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中，你可以指定应用程序所需的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本。 因此，如果要使用此版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 继续开发早期版本中开始的项目，则无需更改框架目标。 你还可以创建包含面向不同版本框架的项目的解决方案。 框架目标还有助于确保应用程序仅使用指定的框架版本中可用的功能。

> [!TIP]
> 你还可以针对不同平台确定目标应用程序。 有关详细信息，请参阅[多目标](../msbuild/msbuild-multitargeting-overview.md)

## <a name="framework-targeting-features"></a>框架目标功能
 框架目标包含下列功能：

- 打开针对 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 早期版本的项目时，[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 可自动升级项目或者保持目标不变。

- 创建项目时，可指定要面向的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本。

- 可更改被现有项目视为目标的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 的版本。

- 可在同一解决方案的各项目中将不同的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本视为目标。

- 更改项目所面向的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本时，[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 会对引用和配置文件进行任何所需更改。

  处理针对 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 早期版本的项目时，Visual Studio 会对开发环境进行如下动态更改：

- 筛选“新建项目”  对话框、“添加新项”  对话框、“添加新引用”  对话框和“添加服务引用”  对话框中的项，以忽略在目标版本中不可用的选项。

- 在“工具箱”  中筛选自定义控件，以删除在目标版本中不可用的控件，并在多个控件可用时仅显示最新版本。

- 对 IntelliSense 进行筛选，以忽略在目标版本中不可用的语言功能。

- 筛选“属性”  窗口中的属性，以忽略在目标版本中不可用的属性。

- 筛选菜单选项以忽略在目标版本中不可用的选项。

- 对于生成，Visual Studio 使用适用于目标版本的编译器版本和编译器选项。

> [!NOTE]
> 框架目标不保证应用程序可正常运行。 必须对应用程序进行测试，以确保其能够针对目标版本运行。 无法面向版本早于 .NET Framework 2.0 的 Framework。

## <a name="selecting-a-target-framework-version"></a>选择目标框架版本
 创建项目时，请在“新建项目”  对话框中选择目标 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本。 根据选定内容对可用项目模板列表进行筛选。 对于现有项目，可在项目属性对话框中更改目标 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本。 有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。

> [!NOTE]
> 在 Visual Studio Express 版中，不能通过“新建项目”  对话框设置目标框架。

## <a name="resolving-system-and-user-assembly-references"></a>解析系统和用户程序集引用
 若要以 .NET Framework 版本为目标，必须先安装相应的程序集引用。 .NET Framework 2.0 版、3.0 版和 3.5 版的程序集引用包含在 .NET Framework 3.5 SP1 中，可从 [Microsoft 下载中心、Microsoft Visual Studio](https://www.microsoft.com/download/details.aspx?id=25150) 网站进行下载。 也可在 [Visual Studio 下载](http://go.microsoft.com/fwlink/?LinkId=179687)网站下载 .NET Framework 3.5 Client Profile、.NET Framework 4、.NET Framework 4 Client Profile 和 Silverlight 的程序集引用。

> [!NOTE]
> .NET Framework 客户端配置文件是 .NET Framework 的子集，可提供一组有限的库和功能。 有关客户端配置文件的详细信息，请参阅 [.NET Framework Client Profile](https://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1)。

 “添加引用”  对话框禁用不适合目标 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本的系统程序集，以便不会无意中将它们添加到项目中。 （系统程序集是包括在 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本内的 .dll 文件。）若引用所属的框架版本低于目标版本，则无法解析引用，并且无法添加基于此类引用的控件。 若要启用此类引用，请将项目的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 目标重新设置为包括此引用。  有关详细信息，请参阅[项目设计器简介](https://msdn.microsoft.com/898dd854-c98d-430c-ba1b-a913ce3c73d7)。

 有关程序集引用的详细信息，请参阅[在设计时解析程序集](../msbuild/resolving-assemblies-at-design-time.md)。

## <a name="enabling-linq"></a>启用 LINQ
 当面向 .NET Framework 3.5 或更高版本时，会自动添加对 System.Core 的引用和 System.Linq 的项目级导入（仅 Visual Basic 中）。 若要使用 LINQ 功能，还必须打开 Option Infer（仅 Visual Basic 中）。 如果将目标更改为早期的 .NET Framework 版本，将自动删除相关引用和导入。 有关详细信息，请参阅[如何：创建 LINQ 项目](https://msdn.microsoft.com/library/a929e653-09a3-44be-881f-68ca33f192b2)。

## <a name="see-also"></a>另请参阅
[多定向](../msbuild/msbuild-multitargeting-overview.md)
[ASP.NET Web 项目的 .NET Framework 多定向](https://msdn.microsoft.com/library/8b8145a9-62f6-4fc4-8a83-47b0487cbe76)
[平台兼容性和系统要求](/visualstudio/productinfo/vs2015-compatibility-vs)
