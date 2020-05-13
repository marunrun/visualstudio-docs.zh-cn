---
title: 开始开发可视化工作室扩展 |微软文档
ms.date: 09/18/2017
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 744475e61458f7b91ce08fba4d17046df36f5558
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699740"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>开始开发 Visual Studio 扩展

如果您以前从未编写过 Visual Studio 扩展，您可能有一些问题。 我们在此处列出了一些最常见的。 如果您没有看到要查找的信息，请使用反馈按钮（**此页面有帮助吗？** 屏幕底部）询问您想要什么。

> [!NOTE]
> 本文适用于 Windows 上的可视化工作室。 有关 Mac 的视觉工作室，请参阅[为 Mac 扩展视觉工作室](/visualstudio/mac/extending-visual-studio-mac)。 有关可视化工作室代码，请参阅[可视化工作室代码扩展 API](https://code.visualstudio.com/api)。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>开发 Visual Studio 扩展需要什么软件？

除了可视化工作室之外，您还需要安装 Visual Studio SDK，以便开发可视化工作室扩展。 您可以将 Visual Studio SDK 作为常规设置的一部分安装，也可以稍后安装它。 有关安装可视化工作室 SDK 的详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>我可以使用 Visual Studio 扩展做什么？

天空是想象不同的视觉工作室扩展的极限。 当然，大多数扩展与编写代码有关，但事实并非如此。 以下是您可以构建的扩展类型的一些示例：

- 支持 Visual Studio 中未包含的语言，包括语法着色、IntelliSense 以及编译器和调试支持

- 通过其他模板、代码重构、新对话框或工具窗口扩展核心 IDE 体验的生产力工具

- 针对数据设计或云支持等方案的特定域设计器

有关扩展的示例，请查看[可视化工作室市场](https://marketplace.visualstudio.com/vs)。 许多扩展都是开源的，应用商店包括指向其 GitHub 存储库的链接。

## <a name="which-visual-studio-features-can-i-extend"></a>我可以扩展哪些视觉工作室功能？

从理论上讲，您可以扩展 Visual Studio 的任何部分：菜单、工具栏、命令、窗口、解决方案、项目、编辑器等。

在实践中，我们发现大多数人想要扩展的功能是命令、菜单和工具栏、窗口、IntelliSense 和项目。 以下是相关部分的链接：

- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)：将您自己的项目添加到 Visual Studio 菜单和工具栏。 您可以使用它们启动新的 Visual Studio 功能或您自己的外部帮助程序应用程序。 您还可以为菜单项提供自定义快捷方式。

- [扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)：扩展现有工具窗口或创建自己的工具窗口。 例如，您可以将新属性添加到**属性**，也可以创建新的工具窗口以添加其他功能。

- [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)：将您自己的自定义项添加到为 Visual Studio 语言提供的 IntelliSense 中，或创建新编程语言。 您可以创建新的语句完成、建议和新的 QuickInfo 工具提示。 使用灯泡，您可以添加重构建议和代码修复以支持新的编程语言。

- [扩展项目](../extensibility/extending-projects.md)

- [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)

- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio 独立 Shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a>VSSDK 提供了哪些项目模板？
 两种主要类型的扩展是 VSPackages 和 MEF 扩展。 通常，VSPackage 扩展用于使用或扩展命令、工具窗口和项目的扩展。 MEF 扩展用于扩展或自定义可视化工作室编辑器。

 对于 Visual C++ 和 Visual Basic 扩展，VSSDK 提供了一个空的 VSIX 项目模板，您可以将该模板与创建菜单命令、工具窗口和编辑器扩展的新项目模板一起使用。 您还可以使用此模板打包项目模板、代码段和其他项目，以便分发给其他用户。

 对于C++，VSPackage 向导提供添加菜单命令、工具窗口和自定义编辑器的代码。

 隔离的 Shell 模板用于在 Visual Studio 外壳版本中打包扩展，您可以将其品牌化并分发为您自己的版本。 以下主题演示如何开始使用各种扩展：

- 菜单命令：[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

- 工具窗口：[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)

- 编辑器扩展：[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本 VS 包：[使用 VS 包创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX 项目模板：[开始使用 VSIX 项目模板](../extensibility/getting-started-with-the-vsix-project-template.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>如何获取扩展，以看起来像视觉工作室？
 在[可视化工作室用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中获取为扩展设计 UI 的提示。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>在哪里可以找到 VSSDK 代码的示例？
 上一节中列出的每个链接都有分步演练，演示如何实现特定功能。 您还可以在[Visual Studio 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)的 GitHub 上找到开源 VSSDK 示例。

## <a name="how-can-i-distribute-my-extension"></a>如何分发我的扩展？
 您可以将扩展卡安装在另一台计算机上，也可以将其作为 .vsix 文件发送给朋友，通过双击来安装该文件。 您可以在[运输视觉工作室扩展](../extensibility/shipping-visual-studio-extensions.md)处了解有关 VSIX 软件包的更多。

 您还可以在可视化工作室应用商店上发布扩展，这使得大量视觉工作室客户可以看到它。 有关将扩展打包到应用商店的示例，请参阅[演练：发布可视化工作室扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。 有关在应用商店上发布需要做什么的详细信息，请参阅[Visual Studio 的产品和扩展](/azure/devops/extend/overview?view=vsts)。

## <a name="see-also"></a>请参阅

- [扩展 Visual Studio for Mac](/visualstudio/mac/extending-visual-studio-mac)
- [扩展视觉工作室代码](https://code.visualstudio.com/api)
