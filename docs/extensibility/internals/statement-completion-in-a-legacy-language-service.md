---
title: 旧版语言服务中的语句完成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c6e157505b146b9c1ca37f508311c9e80958be6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322433"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>旧版语言服务中的语句完成
语句完成是依据语言服务可帮助用户完成语言关键字或他们已启动核心编辑器中键入的元素的过程。 本主题讨论语句完成的工作原理以及如何在你的语言服务中实现它。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现的语句结束的新方法的详细信息，请参阅[演练：显示语句完成](../../extensibility/walkthrough-displaying-statement-completion.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="implementing-statement-completion"></a>实现的语句结束
 在核心编辑器中，语句完成后会激活一个特殊的用户界面，以交互方式可以帮助你更轻松和快速编写代码。 语句完成有助于通过显示相关对象或类在需要时可避免您无需记住特定元素，也无需查找帮助参考主题中。

 若要实现的语句结束，您的语言必须具有语句完成触发器，可以分析它。 例如，[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]使用点 （.） 运算符，而[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]使用一个箭头 (->) 运算符。 语言服务可以使用多个触发器来启动语句完成。 在命令筛选器中对这些触发器进行编程。

## <a name="command-filters-and-triggers"></a>命令筛选器和触发器
 命令筛选器拦截触发器或触发器的匹配项。 若要将命令筛选器添加到视图，实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，并将其附加到该视图通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法。 可以使用的相同命令筛选器 (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) 的所有服务方面的语言，例如语句完成、 错误标记和方法的提示。 有关详细信息，请参阅[截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)。

 当在编辑器中输入触发器时 — 具体来说，文本缓冲区 — 语言服务然后调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>方法。 这将导致编辑器以将该 ui，以便用户可以选择从语句完成候选项。 此方法要求您实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>和<xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags>作为参数的标志。 中滚动列表框中显示完成项的列表。 用户继续键入，在列表框内的选择会更新以反映最新字符与最接近类型化。 核心编辑器实现用于语句完成 UI，但语言服务必须实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>接口可定义一组语句的候选完成项。

## <a name="see-also"></a>请参阅
- [截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)