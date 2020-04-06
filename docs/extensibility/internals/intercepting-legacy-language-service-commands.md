---
title: 拦截旧语言服务命令 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5206bced8b4bfae32498434765e5c3f61801b386
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707442"
---
# <a name="intercepting-legacy-language-service-commands"></a>截获旧版语言服务命令
使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时，可以具有文本视图将处理的语言服务拦截命令。 这对于文本视图未管理的语言特定行为很有用。 您可以通过从语言服务向文本视图添加一个或多个命令筛选器来拦截这些命令。

## <a name="getting-and-routing-the-command"></a>获取和路由命令
 命令筛选器是<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>监视某些字符序列或键命令的对象。 您可以将多个命令筛选器与单个文本视图相关联。 每个文本视图都维护一个命令筛选器链。 创建新的命令筛选器后，将筛选器添加到相应文本视图的链中。

 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>上的方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>以将命令筛选器添加到链中。 调用 时<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]返回另一个命令筛选器，您可以将命令筛选器不处理的命令传递给该筛选器。

 对于命令处理，您有以下选项：

- 处理该命令，然后将该命令传递给链中的下一个命令筛选器。

- 处理该命令，不要将命令传递给下一个命令筛选器。

- 不要处理该命令，而是将该命令传递给下一个命令筛选器。

- 忽略该命令。 请勿在当前筛选器中处理它，也不要将其传递到下一个筛选器。

  有关语言服务应处理哪些命令的信息，请参阅[语言服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。
