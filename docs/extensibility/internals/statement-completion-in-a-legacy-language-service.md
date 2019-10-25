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
ms.openlocfilehash: d4c813052892c21a6a3e04560452b503205df117
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723223"
---
# <a name="statement-completion-in-a-legacy-language-service"></a>旧版语言服务中的语句完成
语句完成是语言服务帮助用户完成在核心编辑器中键入的语言关键字或元素的过程。 本主题讨论语句完成的工作原理以及如何在语言服务中实现它。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现语句结束的新方法的详细信息，请参阅[演练：显示语句完成](../../extensibility/walkthrough-displaying-statement-completion.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="implementing-statement-completion"></a>实现语句完成
 在核心编辑器中，语句结束会激活一个特殊的 UI，该 UI 以交互方式帮助您更轻松、更快速地编写代码。 语句完成有助于在需要相关对象或类时显示这些对象或类，这样就不必记住特定元素，也不必在帮助参考主题中查找它们。

 若要实现语句完成，您的语言必须具有语句完成触发器，该触发器可以进行分析。 例如，[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 使用点（.）运算符，而 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 使用箭头（->）运算符。 语言服务可以使用多个触发器来启动语句完成。 这些触发器在命令筛选器中进行编程。

## <a name="command-filters-and-triggers"></a>命令筛选器和触发器
 命令筛选器会截获触发器或触发器的发生次数。 若要向视图添加命令筛选器，请实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口，并通过调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 方法将其附加到视图。 你可以为语言服务的所有方面使用相同的命令筛选器（<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>），如语句完成、错误标记和方法提示。 有关详细信息，请参阅[截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)。

 当在编辑器中输入触发器（具体而言，是文本缓冲区）后，语言服务将调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> 方法。 这将导致编辑器打开 UI，以便用户可以从语句完成候选项中进行选择。 此方法要求将 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.UpdateCompletionFlags> 标志作为参数实现。 完成项列表将显示在滚动列表框中。 用户继续键入内容时，会更新列表框中的选定内容，以反映最接近键入的最新字符的匹配项。 核心编辑器为语句完成实现 UI，但语言服务必须实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口，才能定义语句的候选完成项集。

## <a name="see-also"></a>请参阅
- [截获旧版语言服务命令](../../extensibility/internals/intercepting-legacy-language-service-commands.md)