---
title: 如何：支持传统语言服务大纲 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28396d513c83ed83e2769e75a6020a98b10251b4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707919"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>如何：支持传统语言服务中的大纲
大纲用于展开或折叠文本的不同区域。 不同语言可以以不同的方式定义大纲的使用方式。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现大纲的新方法的更多，请参阅[演练：大纲](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

 下面演示如何支持语言服务的此命令。

## <a name="to-support-outlining"></a>支持大纲

1. 在<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage>语言服务对象上实现。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>当前大纲会话对象以添加新大纲区域。

## <a name="robust-programming"></a>可靠编程
 当用户选择 **"折叠到****大纲"** 菜单上的定义时，IDE 会调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A>您的语言服务。

 调用此方法时，IDE 会传递<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>指针（指向文本缓冲区的指针）和一个<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>（指向当前大纲会话的指针）。

 通过在`rgOutlnReg`参数中指定<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>这些区域，可以调用多个大纲区域的方法。 参数`rgOutlnReg`是一个<xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion>结构。 此过程允许您指定隐藏区域的不同特征，例如特定区域是展开还是折叠。

> [!NOTE]
> 小心隐藏新行字符。 隐藏文本应从第一行的开头扩展到节中最后一行的最后一个字符，使最后一个新行字符可见。

## <a name="see-also"></a>请参阅
- [如何：在旧语言服务中提供隐藏文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [如何：在传统语言服务中提供扩展的大纲支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
