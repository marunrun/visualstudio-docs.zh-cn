---
title: .NET 目标框架
ms.date: 02/06/2018
ms.topic: conceptual
helpviewer_keywords:
- targeting .NET Framework [Visual Studio]
- framework targeting [Visual Studio]
- .NET framework targeting [Visual Studio]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b652c603cd98f9c9ec9366a225971485def187b6
ms.sourcegitcommit: d4920babfc3d24a3fe1d4bf446ed3fe73b344467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67160154"
---
# <a name="framework-targeting-overview"></a>框架定位概述

在 Visual Studio 中，可以指定希望项目面向的 .NET 版本。 框架定位有助于确保应用程序仅使用指定框架版本中可用的功能。 对于在另一台计算机上运行的 .NET Framework 应用，应用程序面向的 Framework 版本必须与计算机上安装的 Framework 版本兼容。

Visual Studio 解决方案可以包含针对不同 .NET 版本的项目。

有关目标框架的详细信息，请参阅[目标框架](/dotnet/standard/frameworks)。

> [!TIP]
> 你还可以针对不同平台确定目标应用程序。 有关详细信息，请参阅[多定向](../msbuild/msbuild-multitargeting-overview.md)。

## <a name="framework-targeting-features"></a>框架目标功能

框架目标包含下列功能：

- 打开面向早期框架版本的项目时，Visual Studio 可自动升级项目或者保持目标不变。

- 创建 .NET Framework 项目时，可指定要面向的 .NET Framework 版本。

- 可以[面向单个项目中的多个框架](/dotnet/standard/frameworks#how-to-specify-target-frameworks)。

- 同一个解决方案中的多个项目可以面向不同的 .NET 版本。

- 可更改现有项目面向的 .NET 版本。

   更改项目面向的 .NET 版本时，Visual Studio 会对引用和配置文件进行任何所需的更改。

处理面向早期框架版本的项目时，Visual Studio 会对开发环境进行如下动态更改：

- 它筛选“添加新项”  对话框、“添加新引用”  对话框和“添加服务引用”  对话框中的项，以忽略在目标版本中不可用的选项。

- 在“工具箱”  中筛选自定义控件，以删除在目标版本中不可用的控件，并在多个控件可用时仅显示最新版本。

- 筛选 IntelliSense，忽略在目标版本中不可用的语言功能  。

- 筛选“属性”窗口中的属性，忽略在目标版本中不可用的属性  。

- 筛选菜单选项，忽略在目标版本中不可用的选项。

- 对于生成，Visual Studio 使用适用于目标版本的编译器版本和编译器选项。

> [!NOTE]
> - 框架目标不保证应用程序可正常运行。 必须对应用程序进行测试，以确保其能够针对目标版本运行。
> - 无法面向低于 .NET Framework 2.0 的框架版本。

## <a name="select-a-target-framework-version"></a>选择目标框架版本

创建 .NET Framework 项目时，可在选择项目模板后，选择目标 .NET Framework 版本。 可用框架的列表包含适用于所选模板类型的已安装框架版本。 对于非 .NET Framework 项目模板（例如，.NET Core 模板），“框架”下拉列表将不显示  。

::: moniker range="vs-2017"

![VS 2017 中的“框架”下拉列表](media/vside-newproject-framework.png)

::: moniker-end

::: moniker range=">=vs-2019"

![VS 2019 中的“框架”下拉列表](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

## <a name="change-the-target-framework"></a>更改目标框架

对于现有的 Visual Basic、C# 或 F# 项目，可在项目属性对话框中更改目标 .NET 版本。 有关如何更改 C++ 项目目标版本的信息，请改为参阅[如何修改目标框架和平台工具集](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)。

1. 在“解决方案资源管理器”  中，打开要更改的项目的右键单击菜单，然后选择“属性”  。

1. 在“属性”窗口的左列中，选择“应用程序”选项卡   。

   ![项目属性应用程序选项卡](../ide/media/vs_slnexplorer_properties_applicationtab.png)

   > [!NOTE]
   > 创建 UWP 应用后，无法更改 Windows 或 .NET 目标版本。

1. 在“目标框架”  列表中，选择所需版本。

1. 在显示的“验证”对话框中，选择“是”  按钮。

   项目将卸载。 项目重载时，将面向刚选择的 .NET 版本。

> [!NOTE]
> 如果代码中包含对非目标 .NET 版本的引用，则在编译或运行代码时可能会显示错误消息。 若要解决这些错误，请修改这些引用。 请参阅 [.NET 定位错误疑难解答](../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)。

> [!TIP]
> 根据目标框架，它可以在项目文件中按下列方式表示：
>
> - 对于 .NET Core 应用：`<TargetFramework>netcoreapp2.1</TargetFramework>`
> - 对于 .NET Standard 应用：`<TargetFramework>netstandard2.0</TargetFramework>`
> - 对于 .NET Framework 应用：`<TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>`

## <a name="resolve-system-and-user-assembly-references"></a>解析系统和用户程序集引用

要面向 .NET 的某个版本，必须首先安装合适的程序集引用。 可以在 [.NET 下载](https://www.microsoft.com/net/download/windows)页下载针对不同 .NET 版本的开发者包。

对于 .NET Framework 项目，“添加引用”对话框会禁用与目标 .NET Framework 版本无关的系统程序集，以免将其意外添加到项目中  。 （系统程序集是包含在 .NET Framework 版本内的 .dll 文件  。）若引用所属的框架版本高于目标版本，则无法解析引用，并且无法添加基于此类引用的控件。 若要启用此类引用，请将项目的 .NET Framework 目标重新设置为包含此引用。

有关程序集引用的详细信息，请参阅[在设计时解析程序集](../msbuild/resolving-assemblies-at-design-time.md)。

## <a name="enable-linq"></a>启用 LINQ

当面向 .NET Framework 3.5 或更高版本时，会自动添加对 System.Core  的引用和 <xref:System.Linq> 的项目级导入（仅 Visual Basic 中）。 若要使用 LINQ 功能，还必须打开 `Option Infer`（仅 Visual Basic 中）。 如果将目标更改为早期的 .NET Framework 版本，将自动删除相关引用和导入。 有关详细信息，请参阅[使用 LINQ](/dotnet/csharp/tutorials/working-with-linq)。

## <a name="see-also"></a>请参阅

- [目标框架](/dotnet/standard/frameworks)
- [多目标 (MSBuild)](../msbuild/msbuild-multitargeting-overview.md)
- [如何：修改目标框架和平台工具集 (C++)](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset)