---
title: 旧版语言服务中的快速信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cc8bfff0903d2ed1554cfd8b3d5b1dcf5cf0fa8a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436658"
---
# <a name="quick-info-in-a-legacy-language-service"></a>旧版语言服务中的快速信息
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

IntelliSense 快速信息显示有关标识符的信息源中，当用户将插入符号放置在标识符中并选择**快速信息**从**IntelliSense**菜单或保存鼠标标识符上方的光标。 这会导致工具提示，显示有关标识符的信息。 此信息通常包括标识符类型。 当调试引擎处于活动状态时，此信息可能包括的当前值。 调试引擎提供表达式的值，而该语言服务处理仅标识符。  
  
 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[演练：显示快速信息工具提示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)。  
  
> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。  
  
 托管的包框架 (MPF) 语言 service 类用于显示的 IntelliSense 快速信息工具提示提供完全支持。 您需要做的就是提供要显示和启用快速信息功能的文本。  
  
 要显示的文本通过调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法分析程序分析原因值为<xref:Microsoft.VisualStudio.Package.ParseReason>。 此通知分析器来获取类型信息 （或任何适合的快速信息工具提示中显示） 中指定的位置标识符<xref:Microsoft.VisualStudio.Package.ParseRequest>对象。 <xref:Microsoft.VisualStudio.Package.ParseRequest>对象是传递给<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法。  
  
 分析器必须分析中的位置的所有内容<xref:Microsoft.VisualStudio.Package.ParseRequest>对象以确定所有标识符的类型。 然后分析器必须在分析请求位置获取的标识符。 最后，分析器必须将传递到该标识符与关联的工具提示数据<xref:Microsoft.VisualStudio.Package.AuthoringScope>对象，以便该对象可以返回从文本<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>方法。  
  
## <a name="enabling-the-quick-info-feature"></a>启用快速信息功能  
 若要启用快速信息功能，必须设置`CodeSense`并`QuickInfo`名为的参数<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>。设置这些属性<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>和<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A>属性。  
  
## <a name="implementing-the-quick-info-feature"></a>实现快速信息功能  
 <xref:Microsoft.VisualStudio.Package.ViewFilter>类处理的 IntelliSense 快速信息操作。 时<xref:Microsoft.VisualStudio.Package.ViewFilter>类接收<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>命令，类将调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法的分析原因<xref:Microsoft.VisualStudio.Package.ParseReason>和时插入符号位置<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>已发送命令。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法分析器必须然后分析到给定位置的源，但然后分析中给定的位置，以确定要显示快速信息工具提示中的标识符。  
  
 大多数分析器执行整个源代码文件的初始分析，并将结果存储在分析树。 当执行完整的分析<xref:Microsoft.VisualStudio.Package.ParseReason>传递给<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法。 然后，其他类型的分析可用的分析树来获取所需的信息。  
  
 例如，分析原因的值<xref:Microsoft.VisualStudio.Package.ParseReason>可以查找在源位置的标识符和要获取类型信息的分析树中查找它。 此类型信息然后传递给<xref:Microsoft.VisualStudio.Package.AuthoringScope>类，并返回<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A>方法。
