---
title: 什么是 Visual Studio 2015 SDK 中的新增功能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c64aac80-a411-463f-b7bd-8b7607a52ece
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1d51474f2e242f764a84edaa9f2712418c859460
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408698"
---
# <a name="what39s-new-in-the-visual-studio-2015-sdk"></a>什么&#39;s Visual Studio 2015 SDK 中的新增功能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio SDK 的 Visual Studio 2015 中，更新，Visual Studio 2015 和 Visual Studio 2017 具有以下新的和更新功能。

## <a name="visual-studio-2017"></a>Visual Studio 2017

从 Visual Studio 2017 中，扫描自定义项目和项模板将无法再执行。 相反，该扩展插件必须提供模板清单文件描述这些模板的安装位置。 Visual Studio 2017 可用于更新您的 VSIX 扩展。 如果部署使用 MSI 扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅[升级自定义项目和项模板的 Visual Studio 2017](/visualstudio/extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017?view=vs-2015)。 模板清单架构记录在[Visual Studio 模板清单架构参考](/visualstudio/extensibility/visual-studio-template-manifest-schema-reference)。

## <a name="vs-2015-sdk-update-1"></a>VS 2015 SDK 更新 1
 Update 1 包括可帮助您很好地配合颜色主题和 Visual Studio 映像服务的扩展工具。

 这些主题正在[VSSDK 实用工具](../extensibility/internals/vssdk-utilities.md)部分：

- [颜色主题工具](../extensibility/internals/color-theming-tools.md)有助于创建和编辑 Visual Studio 的自定义颜色。

- [图像服务工具](../extensibility/internals/image-service-tools.md)，您可以与 Visual Studio 映像清单文件。

## <a name="new-way-to-add-the-visual-studio-sdk-to-visual-studio"></a>新方法，可以将 Visual Studio SDK 添加到 Visual Studio
 从 Visual Studio 2015 开始，不需要单独下载 Visual Studio SDK。 相反，可以将其作为正常安装过程的一部分安装，或者可以选择要将其安装更高版本上。 当打开或创建 VSIX 解决方案时，Visual Studio 会要求你安装 Visual Studio 扩展性工具。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="new-ways-of-creating-extensions"></a>创建扩展的新方法
 从 Visual Studio 2015 SDK，必须创建的扩展，具体取决于哪种编程语言使用的不同选项。

### <a name="visual-c-and-visual-basic"></a>Visual C# 和 Visual Basic
 对于 C# 和 Visual Basic 中，没有一系列完整的项目项模板，可用于创建 Vspackage、 菜单命令、 工具窗口、 编辑器分类器、 编辑器修饰和编辑器边距扩展。 可以添加任何或所有这些标准的 VSIX 项目。 有关详细信息，请参见:

- [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

- [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)

- [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- [使用 VSPackage 建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

     VSPackage 向导不再创建 C# 或 Visual Basic 中的扩展。

### <a name="c"></a>C++
 有关C++，VSPackage 向导支持菜单命令、 工具窗口和自定义编辑器。 中查找它**新的项目**对话框中的**Visual C++ / 可扩展性**。

## <a name="vs-sdk-reference-assemblies-via-nuget"></a>通过 NuGet VS SDK 引用程序集
 对于更高的可移植性和扩展性项目的共享，可以使用 VS SDK 引用程序集的 NuGet 版本。  这些是可在上找到[nuget.org](http://www.nuget.org)由发布[VisualStudioExtensibility](http://www.nuget.org/profiles/VisualStudioExtensibility) ，可以轻松地添加到你的项目或通过 Visual Studio 的解决方案**引用 / 管理 NuGet包**对话框。 可以单独将引用添加到特定的可扩展性的程序集，也可以添加所有 VS SDK 都引用程序集使用 VS SDK 一次[元包](http://www.nuget.org/packages/VSSDK_Reference_Assemblies)。 若要了解有关 NuGet 的详细信息，请参阅[NuGet 概述](http://docs.nuget.org/)并[使用对话框管理 NuGet 程序包](http://docs.nuget.org/Consume/Package-Manager-Dialog)。

 当你使用 VS SDK 引用程序集的 NuGet 版本时，另一个用户不需要安装 VS SDK 以打开并生成你的项目。  NuGet 引用程序集和 VS SDK 生成工具自动将该项目的其计算机上安装。

 VS SDK 项模板其引用时使用 NuGet 和生成工具，以便获取默认情况下 NuGet 的优点。

> [!NOTE]
> 可以继续使用你的项目使用的安装 VS SDK 引用程序集 (位于下\<Visual Studio 安装位置 > \ VSSDK\VisualStudioIntegration\Common\Assemblies) 和可扩展性的现有项目不需要为升级为使用 NuGet 包。  项目**引用 / 添加引用**对话框仍会继续使用已安装 VS SDK 引用程序集。
>
> 如果你想要修改现有项目以使用 NuGet，请参阅[如何：将 VSPackages 迁移到 Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md)具有一节介绍了可扩展性项目更新对 NuGet 包。

## <a name="light-bulbs"></a>灯泡
 Roslyn 项目提供一个编写扩展代码的最令人兴奋的新方法。 有关详细信息，请参阅[Roslyn](https://github.com/dotnet/Roslyn)。

 电灯泡是附带 VSSDK 的新功能。 它们是使用 Visual Studio 编辑器中，展开此项可显示的代码重构操作或内置代码分析器所发现的问题的修补程序的一组的图标。 有关详细信息，请参见[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)。

## <a name="updated-user-experience-guidelines"></a>已更新的用户体验指南
 用于 Visual Studio 中设计新的扩展或功能？ 请查看更新和扩展[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。  您会发现[颜色令牌](../extensibility/ux-guidelines/shared-colors-for-visual-studio.md)，[字号](../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)，[对话框布局规范](../extensibility/ux-guidelines/layout-for-visual-studio.md)，和你需要将新 UI 与 Visual Studio 无缝集成其他指南。
