---
title: 如何：支持旧版语言服务中的大纲显示 |Microsoft Docs
description: 了解如何在旧版语言服务中为大纲显示、扩展或折叠不同的文本区域提供支持。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: c9d1d7b7a74b6565c666e4d5e3293caaef3c7732
ms.sourcegitcommit: 2f964946d7044cc7d49b3fc10b413ca06cb2d11b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761317"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>如何：支持旧版语言服务中的大纲显示
大纲用于展开或折叠不同的文本区域。 使用大纲显示的方式可以通过不同的语言以不同的方式定义。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现大纲显示的新方式的详细信息，请参阅 [演练：大纲显示](../../extensibility/walkthrough-outlining.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

 下面演示了如何为语言服务支持此命令。

## <a name="to-support-outlining"></a>支持大纲显示

1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage>在语言服务对象上实现。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>在当前大纲显示会话对象上调用来添加新的大纲区域。

## <a name="robust-programming"></a>可靠编程
 当用户选择 "**大纲**" 菜单上的 "**折叠到定义**" 时，IDE 将对 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> 语言服务进行调用。

 调用此方法时，IDE 会将指针传入 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> (指向文本缓冲区的指针) 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> (指向当前大纲显示会话) 的指针。

 可以 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 通过在参数中指定这些区域，为多个大纲区域调用方法 `rgOutlnReg` 。 `rgOutlnReg`参数为 <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> 结构。 此过程允许您指定隐藏区域的不同特征，例如是否展开或折叠特定区域。

> [!NOTE]
> 请小心隐藏新行字符。 隐藏的文本应该从第一行的开头到节中最后一行的最后一个字符，并使最后的新行字符可见。

## <a name="see-also"></a>请参阅
- [如何：在旧版语言服务中提供隐藏的文本支持](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [如何：提供旧版语言服务中的扩展大纲支持](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
