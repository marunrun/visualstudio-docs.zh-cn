---
title: 语言服务和编辑器扩展入门 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4c4278679cabb72e9d06f79c1668e7546f24194d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703761"
---
# <a name="getting-started-with-language-service-and-editor-extensions"></a>语言服务和编辑器扩展入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器扩展可用于将语言服务功能，例如大纲显示、 大括号匹配、 IntelliSense 和灯泡添加到您自己的编程语言或任何内容类型。 此外可以自定义外观和行为的 Visual Studio 编辑器中，例如着色、 边距、 修饰和其他可视元素的文本。 您还可以定义自己的类型的内容，并指定的外观和行为的内容将显示的文本视图。  
  
 若要开始编写编辑器扩展，使用 Visual Studio SDK 的一部分安装的编辑器项目模板。 Visual Studio SDK 是一可下载的工具，有助于轻松地开发 Visual Studio 扩展，通过使用 Vspackage 或通过使用 Managed Extensibility Framework (MEF)。  
  
> [!NOTE]
> 有关 Visual Studio SDK 的详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
 我们建议你了解以下概念和技术编写您自己的编辑器扩展插件之前。  
  
## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>Windows Presentation Foundation (WPF) 和编辑器扩展  
 Visual Studio 编辑器用户界面 (UI) 通过使用 Windows Presentation Foundation (WPF) 实现。 WPF 提供了丰富的视觉体验和业务逻辑分离开来代码的可视方面的一致的编程模型。 创建编辑器扩展时，可以使用多个 WPF 元素和功能。 有关详细信息，请参阅[Windows Presentation Foundation](https://msdn.microsoft.com/library/f667bd15-2134-41e9-b4af-5ced6fafab5d)。  
  
## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>Managed 的 Extensibility Framework (MEF) 和编辑器扩展  
 在 Visual Studio 编辑器使用 Managed Extensibility Framework (MEF) 来管理其组件和扩展。 MEF 还允许开发人员轻松地创建主机应用程序类似于 Visual Studio 的扩展。 在此框架中，定义根据 MEF 协定的扩展，并将其导出为 MEF 组件部分。 主机应用程序通过查找、 注册它们，并确保其应用到的正确的上下文来管理组件的各部分。  
  
> [!NOTE]
> 在编辑器中 MEF 的详细信息，请参阅[在编辑器中的 Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)。  
  
## <a name="visual-studio-editor-extension-points-and-extensions"></a>Visual Studio 编辑器扩展点和扩展  
 编辑器扩展点是 MEF 组件部分，可以自定义和扩展。 在某些情况下你通过实现接口并将其导出正确的元数据以及扩展的扩展点。 在其他情况下您只需声明扩展并将其导出为特定类型。  
  
 以下是一些基本类型的编辑器扩展：  
  
- 边距和滚动条  
  
- Tags  
  
- 修饰  
  
- 选项  
  
- IntelliSense  
  
  有关编辑器扩展点的详细信息，请参阅[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。  
  
## <a name="deploying-editor-extensions"></a>部署编辑器扩展  
 在 Visual Studio 中，你可以通过添加一个名为到解决方案中，生成解决方案时，source.extension.vsixmanifest 的元数据文件并将二进制文件和清单的副本已知的文件夹中添加到 Visual Studio 部署编辑器扩展。 清单文件用于定义扩展插件 （例如，名称、 作者、 版本和内容类型） 有关的基本情况。 有关 VSIX 清单文件以及如何将扩展部署的详细信息，请参阅[传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。  
  
 当你的计算机上安装扩展时，包括到 Visual Studio 已知的文件夹的子文件夹中的二进制文件和清单。  
  
> [!WARNING]
> 无需担心清单和部署位置的详细信息，如果你使用包含在 Visual Studio 的编辑器可扩展性模板之一。 这些模板包含需注册和部署扩展的所有内容。  
  
## <a name="running-extensions-in-the-experimental-instance"></a>在实验实例中运行扩展  
 通过将其部署在以下实验性文件夹 （在 Windows Vista 和 Windows 7） 中开发扩展时，可以使你的 Visual Studio 的工作版本：  
  
 *%LOCALAPPDATA%* \VisualStudio\10.0Exp\Extensions\\*Company*\\*ExtensionID*  
  
 其中 *%LOCALAPPDATA%* 是登录的用户的名称*公司*是拥有该扩展，该公司的名称并*ExtensionID*是扩展的 ID。  
  
 在扩展部署到实验性的位置时，它在调试模式下运行。 Visual Studio 的第二个实例将启动，并且名为**Microsoft Visual Studio 的实验实例**。  
  
## <a name="managing-extensions"></a>管理扩展  
 中列出了 Visual Studio 扩展**扩展和更新**(在**工具**菜单)。 如果要在实验实例中测试扩展，它会列入**扩展和更新**在实验实例中，但未列出的开发实例中。  
  
 有关详细信息，请参阅[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。  
  
## <a name="using-templates-to-create-editor-extensions"></a>使用模板创建编辑器扩展  
 编辑器模板可用于创建自定义分类器、 在修饰和边距的 MEF 扩展。 有 C# 和 Visual Basic 项目的模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
 VSIX 项目模板还可用于创建扩展插件。 此模板提供了所需部署任何类型的扩展，并包含 source.extension.vsixmanifest 文件中，所需程序集引用和包括使你能够部署的生成任务的项目文件元素扩展插件。 有关详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。  
  
 您还可以创建编辑器的 MEF 组件从 Visual Studio 包扩展。 请参阅下面的演练，有关详细信息：  
  
- [演练：在编辑器扩展中使用 Shell 命令](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)  
  
- [演练：将快捷键与编辑器扩展结合使用](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)  
  
## <a name="see-also"></a>请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
