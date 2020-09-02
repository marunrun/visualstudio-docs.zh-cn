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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65674785"
---
# <a name="extending-the-editor-and-language-services"></a>扩展编辑器和语言服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将语言服务功能 (例如 IntelliSense) 添加到自己的编辑器中，并扩展 Visual Studio 代码编辑器的大多数功能。  有关可以扩展的内容的完整列表，请参阅 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。  
  
 您可以通过使用 (MEF) Managed Extensibility Framework 来扩展大多数编辑器功能。 例如，如果要扩展的编辑器功能是语法着色，则可以编写一个 MEF *组件部件* ，用于定义要为其提供不同着色和如何处理的分类。 编辑器还支持同一功能的多个扩展。  
  
 编辑器表示层基于 Windows Presentation Framework (WPF) 。 WPF 提供了一个图形库用于灵活的文本格式设置，还提供了图形和动画等可视化效果。  
  
 Visual Studio SDK 提供了称为 *填充* 程序的适配器，以支持为早期版本编写的 vspackage。 尽管如此，如果你有现有的 VSPackage，我们建议你将其更新为新技术，以获得更好的性能和可靠性。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|说明|  
|-----------|-----------------|  
|[语言服务和编辑器扩展入门](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|说明如何为编辑器创建扩展。|  
|[编辑器内](../extensibility/inside-the-editor.md)|介绍编辑器的一般结构，并列出它的一些功能。|  
|[编辑器中的 Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)|说明如何将 Managed Extensibility Framework (MEF) 与编辑器一起使用。|  
|[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)|列出编辑器的扩展点。 扩展点表示可以扩展的编辑器功能。|  
|[演练：创建视图修饰、命令和设置（列参考线）](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|演练并说明如何生成一个视图修饰，该修饰绘制列 gudie 行，以帮助你将代码保持在特定的显示宽度。  还介绍了如何读取和写入设置，以及如何声明和实现可从 "命令" 窗口调用的命令。|  
|[编辑器导入](../extensibility/editor-imports.md)|列出扩展可以导入的服务。|  
|[根据编辑器调整旧代码](../extensibility/adapting-legacy-code-to-the-editor.md)|说明用于改编旧代码 (Visual Studio 2010 前) 的不同方法来扩展编辑器。|  
|[迁移旧版语言服务](../extensibility/internals/migrating-a-legacy-language-service.md)|说明如何迁移基于 VSPackage 的语言服务。|  
|[演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|演示如何将内容类型链接到文件扩展名。|  
|[演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)|演示如何向边距添加图标。|  
|[演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)|演示如何使用 *标记* 突出显示文本。|  
|[演练：大纲显示](../extensibility/walkthrough-outlining.md)|演示如何为特定类型的大括号添加大纲显示。|  
|[演练：显示匹配括号](../extensibility/walkthrough-displaying-matching-braces.md)|演示如何突出显示匹配的大括号。|  
|[演练：显示 QuickInfo 工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|演示如何显示描述代码元素（如属性、方法和事件）的 QuickInfo 弹出窗口。|  
|[演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)|演示如何显示用于向有关签名中参数的数量和类型的信息的弹出窗口。|  
|[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)|演示如何实现语句结束。|  
|[演练：实现代码片段](../extensibility/walkthrough-implementing-code-snippets.md)|演示如何实现代码段扩展。|  
|[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|演示如何显示代码建议的浅电灯泡。|  
|[演练：在编辑器扩展中使用 Shell 命令](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|演示如何将 VSPackage 中的菜单命令与 MEF 组件相关联。|  
|[演练：在编辑器扩展中使用快捷键](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|演示如何将 VSPackage 中的菜单快捷方式与 MEF 组件相关联。|  
|[Managed Extensibility Framework (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)|提供有关 MEF) Managed Extensibility Framework (的信息。|  
|[Windows Presentation Foundation](https://msdn.microsoft.com/library/f667bd15-2134-41e9-b4af-5ced6fafab5d)|提供有关 WPF) Windows Presentation Foundation (的信息。|  
  
## <a name="reference"></a>参考  
 Visual Studio 编辑器包含以下命名空间。  
  
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
