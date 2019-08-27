---
title: 开始开发扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6d8050ea7447a67f50f42157d57c17d3f1f8a329
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160584"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>开始开发 Visual Studio 扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果您从未书写过 Visual Studio 扩展之前，你可能会出现一些问题。 我们列出了一些最常见的。 如果看不到所需的信息，使用反馈按钮 (**此页面是否有所帮助？** 屏幕底部) 要求所需内容。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>开发 Visual Studio 扩展需要哪些软件？
 您需要安装 Visual Studio 2015 SDK 除了 Visual Studio 2015，才能开发的 Visual Studio 扩展。   可以作为常规安装的一部分安装 Visual Studio 2015 SDK 或更高版本上安装。 有关安装 Visual Studio SDK 的详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>我可以使用 Visual Studio 扩展做何种操作？
 天空是界限谈到设想不同 Visual Studio 扩展。 当然，大多数扩展与编写代码，但它不一定是这种情况。 下面是可以生成的扩展的类型的一些示例：

- 对不包括在 Visual Studio 中，但具有语法着色、 IntelliSense 和编译器和调试支持的语言的支持

- 扩展核心的工作效率工具 IDE 体验的其他模板、 代码重构，则新对话或工具窗口

- 于以下情形： 数据设计或云支持的特定于域的设计器

  有关扩展的示例，请参阅[Visual Studio Marketplace](https://marketplace.visualstudio.com/)。 此外可以看一看[Visual Studio 打开源扩展](https://github.com/Microsoft/extendvs/blob/master/CommunityExtensions.md)。

## <a name="which-visual-studio-features-can-i-extend"></a>可以扩展的 Visual Studio 功能？
 从理论上讲，您可以扩展 Visual Studio 的任何一部分： 菜单、 工具栏、 命令、 windows、 解决方案、 项目、 编辑器和等等。

 在实践中，我们发现，大多数人想要扩展的功能是命令、 菜单和工具栏、 windows、 IntelliSense 和项目。 以下是中的相关章节的链接：

- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)： 将您自己的项添加到 Visual Studio 菜单和工具栏。 可以使用它们以启动 Visual Studio 的新功能或外部帮助器应用程序。 您还可以自定义的快捷方式的菜单项。

- [扩展和自定义工具 Windows](../extensibility/extending-and-customizing-tool-windows.md)： 扩展现有的工具窗口或创建你自己的工具窗口。 例如，可以添加新的属性**属性**，或者可以创建一个新的工具窗口来添加其他功能。

- [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)： 添加自己的自定义 Visual Studio 语言提供的 IntelliSense 或创建新的编程语言的支持。 您可以创建新的语句完成、 建议和新的快速信息工具提示。 使用电灯泡，可以添加重构的建议和代码修补程序，以支持新的编程语言。

- [扩展项目](../extensibility/extending-projects.md)

- [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)

- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio 独立 Shell](../extensibility/visual-studio-isolated-shell.md)

## <a name="BKMK_ProjectTemplate"></a> VSSDK 提供哪些项目模板？
 两个主要类型的扩展是 Vspackage 和 MEF 扩展。 一般情况下，扩展的使用或扩展命令、 工具窗口和项目使用 VSPackage 扩展。 使用 MEF 扩展来扩展或自定义 Visual Studio 编辑器。

 对于 Visual C# 和 Visual Basic 扩展 VSSDK 提供了一个空的 VSIX 项目模板，您可以使用和创建菜单命令、 工具窗口和编辑器扩展的新项模板。 有关详细信息，请参阅[What's New in Visual Studio 2015 SDK](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md)。 此外可以分发给其他用户使用此模板包项目模板、 代码段和其他项目。

 有关C++，VSPackage 向导提供了用于添加菜单命令、 工具窗口和自定义编辑器的代码。

 独立 Shell 模板用于包中的版本的 Visual Studio shell，您可以设置的外观和分发与你自己的扩展插件。 以下主题演示如何开始使用每种类型的扩展：

- 菜单命令：[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

- 工具窗口：[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)

- 编辑器扩展：[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本 Vspackage:[使用 VSPackage 建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX 项目模板：[VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)

- Visual Studio 独立 shell:[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>如何获取我的扩展以类似于 Visual Studio？
 设计为在扩展插件的 UI 获取不错的提示[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>在哪里可以找到 VSSDK 代码的示例？
 每个前面部分中列出的链接具有分步演练说明如何实现特定功能。 您还可以找到开放源代码在 GitHub 上的 VSSDK 示例[Visual Studio 示例](https://aka.ms/vs2015sdksamples)。

## <a name="how-can-i-distribute-my-extension"></a>如何分发 my 扩展？
 可以在另一台计算机上安装扩展，也可以通过双击安装.vsix 文件以将其发送到您的朋友。 您可以了解有关在 VSIX 包的详细信息[传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

 此外可以发布您的扩展 Visual Studio 库，使其向大量 Visual Studio 客户可见。 针对库打包扩展的示例，请参阅[演练：发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。 有关需要执行的操作在库发布的详细信息，请参阅[Visual Studio 的产品和扩展](https://visualstudiogallery.msdn.microsoft.com/)。
