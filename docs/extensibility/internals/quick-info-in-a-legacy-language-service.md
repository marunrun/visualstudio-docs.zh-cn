---
title: 旧版语言服务中的快速信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d070c607313b406f036a5b6f071eaa371070408
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705934"
---
# <a name="quick-info-in-a-legacy-language-service"></a>旧版语言服务中的快速信息
IntelliSense "快速信息" 显示有关源中的标识符的信息。当用户将插入符号置于标识符中，并从**IntelliSense**菜单选择 "**快速信息**" 或将鼠标光标停留在标识符上时，将显示有关源中的标识符的信息。 这会导致出现一个工具提示，其中包含有关标识符的信息。 此信息通常由标识符类型组成。 当调试引擎处于活动状态时，此信息可能包含当前值。 调试引擎提供表达式值，而语言服务仅处理标识符。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [演练：显示 QuickInfo 工具提示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

 管理包框架 (MPF) 语言服务类为显示 IntelliSense 快速信息工具提示提供完全支持。 只需提供要显示的文本并启用快速信息功能。

 要显示的文本是通过调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法分析器，通过分析原因值获取的 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 此原因通知分析器 (获取类型信息，或获取要在 "快速信息工具提示" 中显示的任何内容（在对象中指定的位置的标识符) <xref:Microsoft.VisualStudio.Package.ParseRequest> 。 <xref:Microsoft.VisualStudio.Package.ParseRequest>对象是传递给方法的对象 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 。

 分析器必须分析对象中的位置，以便 <xref:Microsoft.VisualStudio.Package.ParseRequest> 确定所有标识符的类型。 然后，分析器必须在分析请求位置获取标识符。 最后，分析器必须将与该标识符关联的工具提示数据传递给 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 对象，以便对象可以从方法返回文本 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> 。

## <a name="enabling-the-quick-info-feature"></a>启用快速信息功能
 若要启用 "快速信息" 功能，您必须设置的 `CodeSense` 和 `QuickInfo` 命名参数 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 。这些属性设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> 和 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A> 属性。

## <a name="implementing-the-quick-info-feature"></a>实现 "快速信息" 功能
 <xref:Microsoft.VisualStudio.Package.ViewFilter>类处理 IntelliSense 快速信息操作。 当 <xref:Microsoft.VisualStudio.Package.ViewFilter> 类收到命令时 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> ，类会调用方法， <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 并在命令发送时，通过的分析原因 <xref:Microsoft.VisualStudio.Package.ParseReason> 和插入符号的位置 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>然后，方法分析器必须将源分析到给定位置，然后在给定位置分析标识符，以确定要在快速信息工具提示中显示的内容。

 大多数分析程序对整个源文件执行初始分析并将结果存储在分析树中。 传递给方法时，将执行完整的分析 <xref:Microsoft.VisualStudio.Package.ParseReason> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 。 然后，其他类型的分析可以使用分析树获取所需的信息。

 例如，解析原因值 <xref:Microsoft.VisualStudio.Package.ParseReason> 可以在源位置找到标识符，并在分析树中查找它以获取类型信息。 然后，将此类型信息传递给 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 类，并由 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> 方法返回。
