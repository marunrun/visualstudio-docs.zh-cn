---
title: 提供支持语言服务中的大纲显示 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], outlining support
- language services, supporting outlining
- outlining, supporting
ms.assetid: df759e89-8193-418c-8038-6626304d387b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 13bfa8abacbd8f9bd4b604c5a2389981c192b86e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312138"
---
# <a name="how-to-provide-expanded-outlining-support-in-a-legacy-language-service"></a>如何：提供旧版语言服务中的展开大纲显示支持
有两个选项用于扩展对你超出支持的语言的大纲显示支持**折叠到定义**命令。 可以添加控制编辑器的大纲区域，并添加客户端控制大纲区域。

## <a name="adding-editor-controlled-outline-regions"></a>添加编辑器控制大纲区域
 使用此方法创建大纲区域，然后允许编辑器来处理是否展开该区域时，折叠状态，等等。 提供的大纲显示支持的两个选项，此选项是最不可靠。 对于此选项，您创建一个新的大纲区域通过指定的跨度的文本使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>。 创建此区域后，编辑器由控制其行为。 使用以下过程来实现控制编辑器的大纲区域。

### <a name="to-implement-an-editor-controlled-outline-region"></a>若要实现控制编辑器的大纲区域

1. 调用`QueryService`为 <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>

     这将返回一个指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>、 传入针对给定的文本缓冲区的指针。 这将返回一个指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>缓冲区的对象。

3. 调用<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>上<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>指向的指针为<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession>。

4. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A>以添加一个或更多新一次大纲区域。

     此方法允许您指定的文本轮廓，现有的大纲区域是删除还是保留，和大纲区域是展开还是折叠默认情况下是否的跨度。

## <a name="add-client-controlled-outline-regions"></a>添加客户端控制大纲区域
 使用这种方法对实现客户端控制 （或明智） 的大纲显示之类的由[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]语言服务。 若要销毁旧的大纲区域变得无效时，并根据需要创建新的大纲区域，用于管理其自己的大纲显示的语言服务监视文本缓冲区的内容。

### <a name="to-implement-a-client-controlled-outline-region"></a>若要实现客户端控制大纲区域

1. 调用`QueryService`为<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>。 这将返回一个指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>、 传入针对给定的文本缓冲区的指针。 这将确定是否隐藏的文本已存在的会话的缓冲区。

3. 如果文本会话已存在，则不需要创建一个，并指向现有<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>返回对象。 使用此指针来枚举和创建大纲区域。 否则，调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>创建隐藏的文本，会话的缓冲区。 一个指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>返回对象。

    > [!NOTE]
    > 当您调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>，可以指定一个隐藏的文本，客户端 (即，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>对象)。 此客户端会通知你时隐藏文本或大纲区域是展开还是折叠的用户。

4. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>结构) 参数：指定的值<xref:Microsoft.VisualStudio.TextManager.Interop.HIDDEN_REGION_TYPE>中`iType`的成员<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构，以指示要创建大纲区域，而不是隐藏的区域。 指定区域是否受客户端管理，或以编辑器控制`dwBehavior`的成员<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构。 智能的大纲显示实现可以混合的编辑器和客户端控制大纲区域。 指定大纲区域处于折叠状态时，如"..."，在显示的横幅文本`pszBanner`的成员<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构。 隐藏区域的编辑器的默认横幅文本为"..."。