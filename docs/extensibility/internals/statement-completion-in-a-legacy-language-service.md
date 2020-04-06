---
title: 传统语言服务中的语句完成 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- statement completion
- language services, statement completion
ms.assetid: 617439dc-3f0e-4e5f-b346-3e4e7fcf3c1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbeb360cf5bc0f74d6b2d9b93086382dd35da988
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704945"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>旧版语言服务中的语句完成
语句完成是语言服务帮助用户完成他们已开始在核心编辑器中键入的语言关键字或元素的过程。 本主题讨论语句完成的工作原理以及如何在语言服务中实现它。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语句完成的新方法的更多，请参阅[演练：显示语句完成](../../extensibility/walkthrough-displaying-statement-completion.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="implementing-statement-completion"></a>实现声明完成
 在核心编辑器中，语句完成激活了一个特殊的 UI，该 UI 以交互方式帮助您更轻松、更快速地编写代码。 语句完成有助于在需要时显示相关对象或类，从而避免记住特定元素或在帮助参考主题中查找它们。

 要实现语句完成，您的语言必须具有语句完成触发器，可以对其进行分析。 例如，[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]使用点 （.） 运算符，而[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]使用箭头 （->） 运算符。 语言服务可以使用多个触发器启动语句完成。 这些触发器在命令筛选器中编程。

## <a name="command-filters-and-triggers"></a>命令筛选器和触发器
 命令筛选器可拦截触发器或触发器的发生。 要将命令筛选器添加到视图，请<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现接口并通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法将其附加到视图。 可以对语言服务的所有方面使用相同的命令筛选器<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>（ ， 例如语句完成、错误标记和方法提示）。 有关详细信息，请参阅[拦截旧语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)。

 在编辑器中输入触发器时（特别是文本缓冲区），您的语言服务将调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>该方法。 这将导致编辑器打开 UI，以便用户可以从语句完成候选项中进行选择。 此方法要求您实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>和<xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags>标志作为参数。 完成项列表将显示在滚动列表框中。 当用户继续键入时，列表框中的选择将更新以反映与键入的最新字符最接近的匹配项。 核心编辑器实现 UI 以完成语句，但语言服务必须实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>接口，为语句定义一组候选完成项。

## <a name="see-also"></a>请参阅
- [截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)
