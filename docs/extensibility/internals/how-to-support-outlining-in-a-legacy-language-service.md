---
title: 如何：支持旧版语言服务中的大纲显示 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6f79f98ede5c28f8e3acb682ebe8f23e4dc4f72e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312042"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>如何：支持旧版语言服务中的大纲显示
使用大纲显示展开或折叠的文本的不同区域。 使用方式大纲显示可通过不同的语言以不同的方式定义。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现大纲显示的新方法的详细信息，请参阅[演练：大纲显示](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

 以下演示如何为你的语言服务支持此命令。

## <a name="to-support-outlining"></a>若要支持大纲显示

1. 实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage>你语言的服务对象。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>上当前的大纲显示会话对象，若要添加新的大纲区域。

## <a name="robust-programming"></a>可靠编程
 如果用户选择**折叠到定义**上**大纲显示**菜单中，IDE 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A>语言服务上。

 调用此方法时，IDE 将传入<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>指针 （指向文本缓冲区的指针） 和一个<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>（指向当前大纲显示会话的指针）。

 您可以调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>方法通过指定这些区域中的多个大纲区域`rgOutlnReg`参数。 `rgOutlnReg`参数是<xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion>结构。 此过程允许您指定的隐藏区域，如是否展开或折叠某一特定区域的不同特征。

> [!NOTE]
> 谨慎隐藏新行字符。 隐藏的文本，应将扩展从第一个行的开头到最后一个字符的一个部分中，仅显示最后一个新行字符的最后一行。

## <a name="see-also"></a>请参阅
- [如何：提供旧版语言服务中的隐藏的文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [如何：提供旧版语言服务中的展开大纲显示支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)