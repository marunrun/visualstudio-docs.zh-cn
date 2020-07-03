---
title: 在语言服务中提供大纲支持 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 450ef1430e86467d116cc635a27600756bc36075
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905287"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>如何：提供旧版语言服务中的扩展大纲支持
有两个选项可用于扩展对语言的大纲支持，但不支持 "**折叠到定义**" 命令。 可以添加编辑器控制的大纲区域并添加客户端控制的大纲区域。

## <a name="adding-editor-controlled-outline-regions"></a>添加编辑器控制的大纲区域
 使用此方法创建大纲区域，然后允许编辑器处理该区域是否已展开、折叠等。 对于提供大纲支持的两个选项，此选项是最不可靠的。 对于此选项，你可以使用在指定范围内创建新的大纲区域 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 。 此区域创建完成后，其行为由编辑器控制。 使用以下过程来实现编辑器控制的大纲区域。

### <a name="to-implement-an-editor-controlled-outline-region"></a>实现编辑器控制的大纲区域

1. 调用 `QueryService`<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>

     这会返回指向的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> 。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> ，并传入给定文本缓冲区的指针。 这会返回指向缓冲区的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 对象的指针。

3. <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>在上调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 以获取指向的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> 。

4. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> 以一次添加一个或多个新的大纲区域。

     此方法允许您指定要分级显示的文本范围、是否删除现有的大纲区域，以及大纲区域是否默认展开或折叠。

## <a name="add-client-controlled-outline-regions"></a>添加客户端控制的大纲区域
 使用此方法来实现客户端控制的（或智能）大纲显示，就像 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 语言服务使用的一样。 管理其自己的大纲显示的语言服务会监视文本缓冲区内容，以便在其变为无效时销毁旧的大纲区域，并根据需要创建新的大纲区域。

### <a name="to-implement-a-client-controlled-outline-region"></a>实现客户端控制的大纲区域

1. 调用 `QueryService` <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 。 这会返回指向的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> 。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> ，并传入给定文本缓冲区的指针。 这会确定缓冲区是否已存在隐藏的文本会话。

3. 如果已存在文本会话，则不需要创建一个，并返回指向现有对象的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 。 使用此指针枚举和创建大纲区域。 否则，调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> 以创建缓冲区的隐藏文本会话。 返回指向对象的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 。

    > [!NOTE]
    > 调用时 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> ，可以指定隐藏的文本客户端（即 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient> 对象）。 当用户展开或折叠隐藏的文本或大纲区域时，此客户端将通知您。

4. Call <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> structure）参数：在结构的成员中指定的值， <xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE> `iType` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 以指示正在创建大纲区域，而不是隐藏区域。 指定区域在结构的成员中是客户端控制的还是编辑器控制的 `dwBehavior` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 。 智能大纲显示实现可以混合使用编辑器和客户端控制的大纲区域。 指定在您的大纲区域折叠后显示的横幅文本，如 "..." （在结构的成员中）。 `pszBanner` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 隐藏区域的编辑器默认标题文本为 "..."。
