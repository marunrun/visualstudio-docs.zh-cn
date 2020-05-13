---
title: 开始使用语言服务和编辑器扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7894efc477e0c406cf8e85f4d3d31df4f2ef97c5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711314"
---
# <a name="get-started-with-language-service-and-editor-extensions"></a>开始使用语言服务和编辑器扩展
您可以使用编辑器扩展将语言服务功能（如大纲、大括号匹配、IntelliSense 和灯泡）添加到您自己的编程语言或任何内容类型。 您还可以自定义 Visual Studio 编辑器的外观和行为，例如文本着色、边距、修饰和其他可视元素。 您还可以定义自己的内容类型，并指定内容所在的文本视图的外观和行为。

 要开始编写编辑器扩展，请使用作为可视化工作室 SDK 的一部分安装的编辑器项目模板。 Visual Studio SDK 是一组可下载的工具，通过使用 VS 包或使用托管扩展性框架 （MEF），可以更轻松地开发 Visual Studio 扩展。

> [!NOTE]
> 有关可视化工作室 SDK 的详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

 我们建议您在编写自己的编辑器扩展之前了解以下概念和技术。

## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>Windows 演示基础 （WPF） 和编辑器扩展
 可视化工作室编辑器用户界面 （UI） 是通过使用 Windows 演示基础 （WPF） 实现的。 WPF 提供了丰富的视觉体验和一致的编程模型，将代码的可视方面与业务逻辑分开。 创建编辑器扩展时，可以使用许多 WPF 元素和功能。 有关详细信息，请参阅[Windows 演示文稿基础](/dotnet/framework/wpf/index)。

## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>托管扩展性框架 （MEF） 和编辑器扩展
 可视化工作室编辑器使用托管扩展框架 （MEF） 来管理其组件和扩展。 MEF 还允许开发人员更轻松地为 Visual Studio 等主机应用程序创建扩展。 在此框架中，您可以根据 MEF 协定定义扩展，并将其导出为 MEF 组件部件。 主机应用程序通过查找组件、注册组件并确保它们应用于正确的上下文来管理组件部件。

> [!NOTE]
> 有关编辑器中的 MEF 的详细信息，请参阅[编辑器中的托管扩展性框架](../extensibility/managed-extensibility-framework-in-the-editor.md)。

## <a name="visual-studio-editor-extension-points-and-extensions"></a>可视化工作室编辑器扩展点和扩展
 编辑器扩展点是可以自定义和扩展的 MEF 组件部件。 在某些情况下，您可以通过实现接口并将其与正确的元数据一起导出来扩展扩展点。 在其他情况下，您只是声明一个扩展并将其导出为特定类型。

 以下是编辑器扩展的一些基本类型：

- 边距和滚动条

- Tags

- 装饰品

- 选项

- IntelliSense

  有关编辑器扩展点的详细信息，请参阅[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。

## <a name="deploying-editor-extensions"></a>部署编辑器扩展
 在 Visual Studio 中，您可以通过向解决方案添加名为*source.扩展.vsixmanifest*的元数据文件来部署编辑器扩展，生成解决方案，然后在 Visual Studio 已知的文件夹中添加二进制文件和清单的副本。 清单文件定义有关扩展名的基本事实（例如，名称、作者、版本和内容类型）。 有关 VSIX 清单文件以及如何部署扩展的详细信息，请参阅[船舶可视化工作室扩展](../extensibility/shipping-visual-studio-extensions.md)。

 在计算机上安装扩展时，将二进制文件和清单包含在 Visual Studio 已知的文件夹的子文件夹中。

> [!WARNING]
> 如果使用 Visual Studio 中包含的编辑器扩展模板之一，则不必担心清单和部署位置的详细信息。 模板包含注册和部署扩展所需的所有内容。

## <a name="run-extensions-in-the-experimental-instance"></a>在实验实例中运行扩展
 在开发扩展时，您可以通过在以下实验文件夹中（在 Windows Vista 和 Windows 7 上）部署该扩展来隔离工作版本的 Visual Studio：

 *[%本地应用数据%][VisualStudio]10.0Exp_扩展\\[公司]\\[扩展 ID]*

 *其中 %LOCALAPPDATA%* 是登录用户的名称，*公司*是拥有扩展名的公司的名称，*扩展 ID*是扩展的 ID。

 将扩展部署到实验位置时，它将在调试模式下运行。 视觉工作室的第二个实例启动，并命名为**微软视觉工作室-实验实例**。

## <a name="manage-extensions"></a>管理扩展
 "扩展 **"和"更新**"（在 **"工具"** 菜单上）中列出了可视化工作室的扩展。 如果要在实验实例中测试扩展，它将在实验实例中的**扩展和更新**中列出，但在开发实例中未列出。

 有关详细信息，请参阅[查找和使用可视化工作室扩展](../ide/finding-and-using-visual-studio-extensions.md)。

## <a name="use-templates-to-create-editor-extensions"></a>使用模板创建编辑器扩展
 可以使用编辑器模板创建自定义分类器、修饰和边距的 MEF 扩展。 C# 和可视化基本项目都有模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

 您还可以使用 VSIX 项目模板创建扩展。 此模板仅提供部署任何类型的扩展所需的元素，并包括*source.扩展.vsixmanifest*文件、所需的程序集引用以及包含允许您部署扩展的生成任务的项目文件。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

 您还可以从可视化工作室包扩展创建编辑器 MEF 组件。 有关详细信息，请参阅以下演练：

- [演练：使用具有编辑器扩展的 shell 命令](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)

- [演练：使用带有编辑器扩展的快捷键](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
