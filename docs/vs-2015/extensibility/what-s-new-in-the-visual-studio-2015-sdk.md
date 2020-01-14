---
title: Visual Studio 2015 SDK 的新增功能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c64aac80-a411-463f-b7bd-8b7607a52ece
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d47e40a5c38eeb7898aa179282fa55bbe17ef1d5
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917335"
---
# <a name="what39s-new-in-the-visual-studio-2015-sdk"></a>Visual&#39;STUDIO 2015 SDK 中的新增功能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio SDK 具有以下新功能和更新功能，适用于 Visual Studio 2015、Visual Studio 2015 更新和 Visual Studio 2017。

## <a name="visual-studio-2017"></a>Visual Studio 2017

从 Visual Studio 2017 开始，将不再执行对自定义项目和项模板的扫描。 相反，该扩展插件必须提供描述这些模板安装位置的模板清单文件。 可以使用 Visual Studio 2017 更新 VSIX 扩展。 如果使用 MSI 部署扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅[升级自定义 Visual Studio 项目和项模板 2017](/visualstudio/extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017?view=vs-2015)。 [Visual Studio 模板清单架构参考](/visualstudio/extensibility/visual-studio-template-manifest-schema-reference)中介绍了模板清单架构。

## <a name="vs-2015-sdk-update-1"></a>VS 2015 SDK Update 1
 Update 1 包含的工具可帮助您更好地处理颜色主题和 Visual Studio 图像服务。

 这些主题位于 " [VSSDK 实用工具](../extensibility/internals/vssdk-utilities.md)" 部分下面：

- [颜色主题工具](../extensibility/internals/color-theming-tools.md)可帮助你为 Visual Studio 创建和编辑自定义颜色。

- [映像服务工具](../extensibility/internals/image-service-tools.md)使你可以使用 Visual Studio 映像清单文件。

## <a name="new-way-to-add-the-visual-studio-sdk-to-visual-studio"></a>将 Visual Studio SDK 添加到 Visual Studio 的新方法
 从 Visual Studio 2015 开始，无需单独下载 Visual Studio SDK。 相反，你可以将其作为常规安装过程的一部分进行安装，也可以选择在以后安装它。 打开或创建 VSIX 解决方案时，Visual Studio 将要求你安装 Visual Studio 扩展性工具。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="new-ways-of-creating-extensions"></a>新的扩展创建方法
 从 Visual Studio 2015 SDK 开始，根据所使用的编程语言，你可以使用不同的选项来创建扩展。

### <a name="visual-c-and-visual-basic"></a>Visual C# 和 Visual Basic
 对于C#和 Visual Basic，可以使用一系列完整的项目项模板来创建 vspackage、菜单命令、工具窗口、编辑器分类器、编辑器修饰和编辑器边距扩展。 您可以将所有这些或全部添加到标准 VSIX 项目中。 有关详细信息，请参阅：

- [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

- [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)

- [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- [使用 VSPackage 建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

     VSPackage 向导不再在或 Visual Basic 中C#创建扩展。

### <a name="c"></a>C++
 对于C++，VSPackage 向导支持菜单命令、工具窗口和自定义编辑器。 在**Visual C++ /扩展性**的 "**新建项目**" 对话框中查找它。

## <a name="vs-sdk-reference-assemblies-via-nuget"></a>VS SDK Reference 程序集通过 NuGet
 为了提高可移植性和可共享的扩展性项目，可以使用 VS SDK 引用程序集的 NuGet 版本。  这些功能在[VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility)发布的[nuget.org](https://www.nuget.org/)上可用，并可通过 Visual Studio 的 "**引用/管理 nuget 包**" 对话框轻松添加到项目或解决方案中。 您可以使用 VS SDK[元包](https://www.nuget.org/packages/VSSDK_Reference_Assemblies)一次添加对特定扩展性程序集的单独引用或添加所有 VS sdk 引用程序集。 若要了解有关 NuGet 的详细信息，请参阅[Nuget 概述](/nuget/)和[使用对话框管理 nuget 包](/nuget/consume-packages/install-use-packages-visual-studio)。

 使用 VS SDK 引用程序集的 NuGet 版本时，其他用户无需安装 VS SDK 即可打开和生成项目。  NuGet 引用程序集和 VS SDK 生成工具会自动安装在其计算机上用于该项目。

 VS SDK 项模板为其引用和生成工具使用 NuGet，因此默认情况下会获得 NuGet 的优点。

> [!NOTE]
> 你可以继续将 VS SDK 安装的引用程序集与你的项目（位于 \<Visual Studio 安装位置 > \ VSSDK\VisualStudioIntegration\Common\Assemblies）下，并且现有的扩展性项目无需升级便可使用 NuGet 包。  "项目**引用/添加引用**" 对话框继续使用 VS SDK 安装的引用程序集。
>
> 如果要修改现有项目以使用 NuGet，请参阅[如何：将 Vspackage 迁移到 Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md) ，其中包含有关将扩展性项目更新到 NuGet 包的部分。

## <a name="light-bulbs"></a>浅电灯泡
 Roslyn 项目提供了编写扩展代码的最令人兴奋的新方法之一。 有关详细信息，请参阅[Roslyn](https://github.com/dotnet/Roslyn)。

 轻型电灯泡是 VSSDK 随附的一项新功能。 它们是 Visual Studio 编辑器中使用的图标，可展开以显示由内置代码分析器标识的问题的一组代码重构操作或修补程序。 有关详细信息，请参阅[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)。

## <a name="updated-user-experience-guidelines"></a>更新的用户体验指南
 设计 Visual Studio 的新扩展或功能？ 查看更新和扩展的[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。  你将找到[颜色标记](../extensibility/ux-guidelines/shared-colors-for-visual-studio.md)、[字体大小](../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)、[对话框布局规范](../extensibility/ux-guidelines/layout-for-visual-studio.md)，以及与 VISUAL Studio 无缝集成新 UI 所需的其他指导。
