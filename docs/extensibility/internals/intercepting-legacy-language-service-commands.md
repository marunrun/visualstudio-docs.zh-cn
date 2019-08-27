---
title: 截获旧版语言服务命令 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3716f02b076bd5ea7ef63135133acffc823a7703
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314946"
---
# <a name="intercepting-legacy-language-service-commands"></a>截获旧版语言服务命令
使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，您可以用来处理文本视图的语言服务截距命令。 这可用于在文本视图不会管理的特定于语言的行为。 可以通过将一个或多个命令筛选器添加到文本视图中，从你的语言服务截获这些命令。

## <a name="getting-and-routing-the-command"></a>获取和路由命令
 命令筛选器是<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>监视特定的字符序列或命令的对象。 可以将多个命令筛选器与单个文本视图相关联。 每个文本视图会保持命令链筛选器。 创建新的命令筛选器后，您将筛选器添加到相应的文本视图的链。

 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>将命令筛选器添加到该链。 当您调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]返回另一个命令筛选器可以向其传递命令筛选器不处理的命令。

 具有命令处理的以下选项：

- 处理命令，然后将该命令到下一个命令筛选器传递链中。

- 处理命令并不传递到下一个命令筛选器的命令。

- 不处理该命令，但将传递到下一个命令筛选器的命令。

- 忽略该命令。 不处理它在当前筛选器，并不将它传递到下一个筛选器。

  语言服务应处理哪些命令有关的信息，请参阅[语言服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。