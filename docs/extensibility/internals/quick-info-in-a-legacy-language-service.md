---
title: 传统语言服务中的快速信息 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705934"
---
# <a name="quick-info-in-a-legacy-language-service"></a>旧版语言服务中的快速信息
IntelliSense 快速信息显示有关源中标识符的信息，当用户将图子放在标识符中并从**IntelliSense**菜单中选择 **"快速信息"** 或将鼠标光标放在标识符上时。 这将导致工具提示显示与标识符的信息。 此信息通常由标识符类型组成。 当调试引擎处于活动状态时，此信息可能包含当前值。 调试引擎提供表达式值，而语言服务仅处理标识符。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[演练：显示快速信息工具提示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

 托管包框架 （MPF） 语言服务类为显示 IntelliSense 快速信息工具提示提供完全支持。 所有你需要做的是提供要显示的文本，并启用快速信息功能。

 要显示的文本是通过调用具有 分析原因值<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>的方法解析器获得的<xref:Microsoft.VisualStudio.Package.ParseReason>。 此原因告诉解析器在<xref:Microsoft.VisualStudio.Package.ParseRequest>对象中指定的位置获取标识符的类型信息（或任何适合显示在"快速信息"工具提示中显示的信息）。 对象<xref:Microsoft.VisualStudio.Package.ParseRequest>是传递给方法的内容<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>。

 解析器必须解析到<xref:Microsoft.VisualStudio.Package.ParseRequest>对象中位置的所有内容，以确定所有标识符的类型。 然后，解析器必须在解析请求位置获取标识符。 最后，解析器必须将与此标识符关联的工具提示数据传递给<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象，以便对象可以从<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>方法返回文本。

## <a name="enabling-the-quick-info-feature"></a>启用快速信息功能
 要启用"快速信息"功能，必须设置`CodeSense`和`QuickInfo`命名的参数<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>。这些属性设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>和<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A>属性。

## <a name="implementing-the-quick-info-feature"></a>实现快速信息功能
 该<xref:Microsoft.VisualStudio.Package.ViewFilter>类处理"IntelliSense 快速信息"操作。 <xref:Microsoft.VisualStudio.Package.ViewFilter>当类<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>接收命令时，类调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法时具有解析的原因<xref:Microsoft.VisualStudio.Package.ParseReason>和命令发送时<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>的 caret 的位置。 然后<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>，方法解析器必须将源解析为给定位置，然后在给定位置解析标识符，以确定在"快速信息"工具提示中显示的内容。

 大多数解析器对整个源文件进行初始分析，并将结果存储在解析树中。 当传递给<xref:Microsoft.VisualStudio.Package.ParseReason><xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法时，将执行完整的分析。 然后，其他类型的分析可以使用解析树来获取所需的信息。

 例如，的<xref:Microsoft.VisualStudio.Package.ParseReason>解析原因值可以在源位置找到标识符，并在解析树中查找它以获取类型信息。 然后，将此类型信息传递给<xref:Microsoft.VisualStudio.Package.AuthoringScope>类，并由 方法<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>返回。
