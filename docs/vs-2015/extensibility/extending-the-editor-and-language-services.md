---
title: 扩展编辑器和语言服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 085e1b5c1fbfbbaf5649966738f2864e0b72ed35
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674785"
---
# <a name="extending-the-editor-and-language-services"></a>扩展编辑器和语言服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将语言服务功能 （如 IntelliSense) 添加到您自己的编辑器，并扩展 Visual Studio 代码编辑器中的大多数功能。  您可以扩展的完整列表，请参阅[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。  
  
 使用 Managed Extensibility Framework (MEF) 扩展编辑器的大多数功能。 例如，如果你想要扩展的编辑器功能是语法着色，可以编写 MEF*组成部分*，它定义要为其不同的颜色设置和其处理方式的分类。 此编辑器还支持多个扩展的相同功能。  
  
 编辑器的表示层基于 Windows Presentation Framework (WPF)。 WPF 图形库提供的灵活的文本格式设置，并还提供了可视化效果，如图形和动画。  
  
 Visual Studio SDK 提供了名为适配器*填充程序*以支持为早期版本编写的 Vspackage。 不过，如果有现有的 VSPackage，我们建议对新技术，从而获得更好的性能和可靠性更新它。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|描述|  
|-----------|-----------------|  
|[语言服务和编辑器扩展入门](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|说明如何创建编辑器的扩展。|  
|[编辑器内](../extensibility/inside-the-editor.md)|描述在编辑器的常规结构并列出它的某些功能。|  
|[编辑器中的 Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)|介绍如何通过在编辑器中使用 Managed Extensibility Framework (MEF)。|  
|[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)|列出在编辑器的扩展点。 扩展点表示编辑器功能，可以进行扩展。|  
|[演练：创建视图修饰、命令和设置（列参考线）](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|将指导完成并解释了构建视图修饰用于绘制列 gudie 行，以帮助您使代码保持到某些显示宽度。  此外显示了读取和写入设置，以及声明和实现可以在命令窗口中调用的命令。|  
|[编辑器导入](../extensibility/editor-imports.md)|列出扩展可以导入的服务。|  
|[根据编辑器调整旧代码](../extensibility/adapting-legacy-code-to-the-editor.md)|介绍了不同的方式以适应旧代码 (预先 Visual Studio 2010) 来扩展编辑器。|  
|[迁移旧版语言服务](../extensibility/internals/migrating-a-legacy-language-service.md)|介绍如何将迁移基于 VSPackage 语言服务。|  
|[演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|演示如何将内容类型链接到的文件扩展名。|  
|[演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)|演示如何将图标添加到边距。|  
|[演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)|演示如何使用*标记*以突出显示文本。|  
|[演练：大纲显示](../extensibility/walkthrough-outlining.md)|演示如何添加特定类型的大括号的大纲显示。|  
|[演练：显示匹配的括号](../extensibility/walkthrough-displaying-matching-braces.md)|演示如何突出显示匹配大括号。|  
|[演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|演示如何显示介绍的代码如属性、 方法和事件的元素的快速信息弹出窗口。|  
|[演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)|演示如何显示在签名中提供的数量和类型参数的有关信息的弹出窗口。|  
|[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)|演示如何实现的语句结束。|  
|[演练：实现代码片段](../extensibility/walkthrough-implementing-code-snippets.md)|演示如何实现代码片段扩展。|  
|[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|演示如何显示代码建议的灯泡。|  
|[演练：在编辑器扩展中使用 Shell 命令](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|演示如何将菜单命令在 VSPackage 中的与 MEF 组件相关联。|  
|[演练：将快捷键与编辑器扩展结合使用](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|演示如何在 VSPackage 中的菜单快捷方式相关联的 MEF 组件。|  
|[Managed Extensibility Framework (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)|提供有关 Managed Extensibility Framework (MEF) 的信息。|  
|[Windows Presentation Foundation](https://msdn.microsoft.com/library/f667bd15-2134-41e9-b4af-5ced6fafab5d)|提供有关 Windows Presentation Foundation (WPF) 的信息。|  
  
## <a name="reference"></a>参考  
 在 Visual Studio 编辑器包括以下命名空间。  
  
 <xref:Microsoft.VisualStudio.Language.Intellisense>  
  
 <xref:Microsoft.VisualStudio.Language.StandardClassification>  
  
 <xref:Microsoft.VisualStudio.Editor>  
  
 <xref:Microsoft.VisualStudio.Text>  
  
 <xref:Microsoft.VisualStudio.Text.Adornments>  
  
 <xref:Microsoft.VisualStudio.Text.Classification>  
  
 <xref:Microsoft.VisualStudio.Text.Differencing>  
  
 <xref:Microsoft.VisualStudio.Text.Document>  
  
 <xref:Microsoft.VisualStudio.Text.Editor>  
  
 <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods>  
  
 <xref:Microsoft.VisualStudio.Text.Formatting>  
  
 <xref:Microsoft.VisualStudio.Text.IncrementalSearch>  
  
 <xref:Microsoft.VisualStudio.Text.Operations>  
  
 <xref:Microsoft.VisualStudio.Text.Outlining>  
  
 <xref:Microsoft.VisualStudio.Text.Projection>  
  
 <xref:Microsoft.VisualStudio.Text.Tagging>  
  
 <xref:Microsoft.VisualStudio.Utilities>
