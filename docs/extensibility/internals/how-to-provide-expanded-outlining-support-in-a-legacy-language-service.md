---
title: 在语言服务中提供概述支持 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 37deafa92477289a2124ecee101dd254e68ef01d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707972"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>如何：在传统语言服务中提供扩展的大纲支持
除了支持 **"折叠到定义"** 命令之外，还有两个选项可以扩展对语言的支持。 您可以添加编辑器控制的大纲区域，并添加客户端控制的大纲区域。

## <a name="adding-editor-controlled-outline-regions"></a>添加编辑器控制的大纲区域
 使用此方法创建大纲区域，然后允许编辑器处理区域是否展开、折叠等。 在提供大纲支持的两个选项中，此选项最不健壮。 对于此选项，使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>在指定的文本范围内创建新的大纲区域。 创建此区域后，其行为由编辑器控制。 使用以下过程实现编辑器控制的大纲区域。

### <a name="to-implement-an-editor-controlled-outline-region"></a>实现编辑器控制的大纲区域

1. 呼叫`QueryService`<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>

     这将返回指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>的指针。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>， 传入给定文本缓冲区的指针。 这将返回指向缓冲区<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>对象的指针。

3. 调用<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>的指针。

4. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>一次添加一个或多个新大纲区域。

     此方法允许您指定要大纲的文本范围、是否删除或保留现有大纲区域，以及大纲区域是默认情况下展开还是折叠。

## <a name="add-client-controlled-outline-regions"></a>添加客户端控制的大纲区域
 使用此方法实现客户端控制（或智能）大纲，如[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]语言服务所使用的大纲。 管理自己的大纲的语言服务会监视文本缓冲区内容，以便在旧大纲区域无效时销毁它们，并根据需要创建新的大纲区域。

### <a name="to-implement-a-client-controlled-outline-region"></a>实现客户端控制的大纲区域

1. 调用`QueryService`<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>。 这将返回指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>的指针。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>， 传入给定文本缓冲区的指针。 这将确定缓冲区是否已存在隐藏文本会话。

3. 如果文本会话已存在，则无需创建一个会话，并返回指向现有<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>对象的指针。 使用此指针枚举并创建轮廓区域。 否则，调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>以创建缓冲区的隐藏文本会话。 返回指向对象的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>指针。

    > [!NOTE]
    > 调用 时<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>，可以指定隐藏文本客户端（即<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>对象）。 当用户展开或折叠隐藏文本或大纲区域时，此客户端将通知您。

4. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>结构）参数：在<xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE>`iType`<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构成员中指定 值以指示您正在创建大纲区域，而不是隐藏区域。 指定区域是客户端控制还是`dwBehavior`<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构成员中的编辑器控制。 智能大纲实现可以包含编辑器和客户端控制的大纲区域的组合。 指定在大纲区域折叠时显示的横幅文本，如`pszBanner`<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构成员中的"..."。 编辑对隐藏区域的默认横幅文本为"..."。
