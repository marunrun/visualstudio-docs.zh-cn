---
title: 扩展编辑器和语言服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 239c638ec32cc0dc2b2e275a5dbe0c4213a3423e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711714"
---
# <a name="extend-the-editor-and-language-services"></a>扩展编辑器和语言服务
您可以将语言服务功能（如 IntelliSense）添加到您自己的编辑器中，并扩展 Visual Studio 代码编辑器的大多数功能。  有关可以扩展的内容的完整列表，请参阅[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。

 您可以使用托管扩展性框架 （MEF） 扩展大多数编辑器功能。 例如，如果要扩展的编辑器功能是语法着色，则可以编写一个 MEF*组件部件*，用于定义需要不同颜色的分类以及您希望它们的处理方式。 编辑器还支持同一功能的多个扩展。

 编辑器表示层基于 Windows 演示文稿框架 （WPF）。 WPF 提供了用于灵活文本格式的图形库，还提供图形和动画等可视化效果。

 Visual Studio SDK 提供称为*hims*的适配器，以支持为早期版本编写的 VS 包。 但是，如果您有现有的 VSPackage，我们建议您将其更新到新技术，以获得更好的性能和可靠性。

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[开始使用语言服务和编辑器扩展](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|说明如何创建编辑器的扩展。|
|[编辑器内部](../extensibility/inside-the-editor.md)|描述编辑器的一般结构，并列出它的一些功能。|
|[编辑器中的托管扩展性框架](../extensibility/managed-extensibility-framework-in-the-editor.md)|说明如何使用托管扩展框架 （MEF） 与编辑器。|
|[语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)|列出编辑器的扩展点。 扩展点表示可扩展的编辑器功能。|
|[演练：创建视图装饰、命令和设置（列参考线）](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|遍通并解释构建一个视图修饰，绘制列引导线，以帮助您将代码保持在特定的显示宽度。  还显示读取和写入设置以及声明和实现可以从命令窗口调用的命令。|
|[编辑器导入](../extensibility/editor-imports.md)|列出扩展可以导入的服务。|
|[将旧代码调整到编辑器](/visualstudio/extensibility/adapting-legacy-code-to-the-editor?view=vs-2015)|解释调整旧版代码（Visual Studio 2010 前）以扩展编辑器的不同方法。|
|[迁移旧语言服务](../extensibility/internals/migrating-a-legacy-language-service.md)|说明如何迁移基于 VSPackage 的语言服务。|
|[演练：将内容类型链接到文件名扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|演示如何将内容类型链接到文件名扩展名。|
|[演练：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)|演示如何向边距添加图标。|
|[演练：突出显示文本](../extensibility/walkthrough-highlighting-text.md)|演示如何使用*标记*突出显示文本。|
|[演练：添加大纲](../extensibility/walkthrough-outlining.md)|演示如何添加特定类型的大括号的大纲。|
|[演练：显示匹配的大括号](../extensibility/walkthrough-displaying-matching-braces.md)|演示如何突出显示匹配的大括号。|
|[演练：显示快速信息工具提示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|演示如何显示描述代码元素（如属性、方法和事件）的 QuickInfo 弹出窗口。|
|[演练：显示签名帮助](../extensibility/walkthrough-displaying-signature-help.md)|演示如何显示提供签名中参数数和类型信息的弹出窗口。|
|[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)|演示如何实现语句完成。|
|[演练：实现代码段](../extensibility/walkthrough-implementing-code-snippets.md)|演示如何实现代码段扩展。|
|[演练：显示灯泡建议](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|演示如何显示灯泡以进行代码建议。|
|[演练：使用具有编辑器扩展的 shell 命令](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|演示如何将 VSPackage 中的菜单命令与 MEF 组件相关联。|
|[演练：使用带有编辑器扩展的快捷键](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|演示如何将 VSPackage 中的菜单快捷方式与 MEF 组件相关联。|
|[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)|提供有关托管扩展性框架 （MEF） 的信息。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|提供有关 Windows 演示文稿基础 （WPF） 的信息。|

## <a name="reference"></a>参考
 Visual Studio 编辑器包括以下命名空间。

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
