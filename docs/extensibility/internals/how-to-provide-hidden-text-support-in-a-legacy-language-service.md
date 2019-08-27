---
title: 提供旧版语言服务中的隐藏的文本支持
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3d1088399256a4d5b16fa269ce022800ed645b1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351029"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>如何：提供旧版语言服务中的隐藏的文本支持
你可以创建大纲区域除了隐藏的文本区域。 隐藏的文本区域可以是客户端控制或编辑器控制和用于完全隐藏的文本区域。 编辑器为水平线条显示隐藏的区域。 这就**仅限脚本**HTML 编辑器中的视图。

## <a name="to-implement-a-hidden-text-region"></a>若要实现隐藏的文本区域

1. 调用`QueryService`为<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>。

     这将返回一个指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>、 传入针对给定的文本缓冲区的指针。 这将确定是否隐藏的文本已存在的会话的缓冲区。

3. 如果已存在，则不需要创建一个，一个指向现有<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>返回对象。 使用此指针来枚举和创建隐藏的文本区域。 否则，调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>创建隐藏的文本，会话的缓冲区。

     一个指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>返回对象。

    > [!NOTE]
    > 当您调用`CreateHiddenTextSession`，可以指定一个隐藏的文本，客户端 (即， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>)。 隐藏的文本或大纲显示展开或折叠的用户时，隐藏的文本，客户端将通知你。

4. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>以添加一个或其他新大纲区域时，指定以下信息在`reHidReg`(<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>) 参数：

    1. 指定的值`hrtConcealed`中`iType`的成员<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构，以指示要创建一个隐藏的区域，而不是大纲区域。

        > [!NOTE]
        > 隐藏的区域处于隐藏状态，编辑器将自动显示要指明其状态的隐藏区域周围的线。

    2. 指定区域是否受客户端管理，或以编辑器控制`dwBehavior`的成员<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构。 智能的大纲显示实现可以包含多个编辑器和客户端控制大纲和隐藏的文本区域。