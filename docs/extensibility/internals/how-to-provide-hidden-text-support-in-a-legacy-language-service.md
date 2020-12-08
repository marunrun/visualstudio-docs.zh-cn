---
title: 提供旧版语言服务中的隐藏文本支持
description: 了解如何通过添加编辑器控制的或客户端控制的隐藏文本区域，在旧版语言服务中提供隐藏的文本支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hidden text, supporting
- editors [Visual Studio SDK], hidden text
- language services, implementing hidden text regions
ms.assetid: 1c1dce9f-bbe2-4fc3-a736-5f78a237f4cc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1f51f8e0c5ca268c1171804f663e5d01bd7c2530
ms.sourcegitcommit: 2f964946d7044cc7d49b3fc10b413ca06cb2d11b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761304"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>如何：在旧版语言服务中提供隐藏的文本支持
除了大纲区域外，还可以创建隐藏的文本区域。 隐藏的文本区域可以是客户端控制的，也可以是由编辑器控制的，用于完全隐藏文本区域。 编辑器将隐藏区域显示为水平线条。 在 HTML 编辑器中，这是 **仅限脚本** 的视图。

## <a name="to-implement-a-hidden-text-region"></a>实现隐藏的文本区域

1. 调用 `QueryService` <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> 。

     这会返回指向的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> 。

2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A> ，并传入给定文本缓冲区的指针。 这会确定缓冲区是否已存在隐藏的文本会话。

3. 如果已存在一个，则不需要创建一个，并返回指向现有对象的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 。 使用此指针可枚举和创建隐藏的文本区域。 否则，调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A> 以创建缓冲区的隐藏文本会话。

     返回指向对象的指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 。

    > [!NOTE]
    > 调用时， `CreateHiddenTextSession` 可以指定隐藏的文本客户端 (， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>) 。 当用户展开或折叠隐藏文本或大纲时，隐藏的文本客户端将通知您。

4. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> 以一次添加一个或多个新的大纲区域，同时在 `reHidReg` () 参数中指定以下信息 <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> ：

    1. 在结构的成员中指定的值， `hrtConcealed` `iType` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 以指示正在创建隐藏区域，而不是大纲区域。

        > [!NOTE]
        > 隐藏隐藏区域后，编辑器会自动显示隐藏区域周围的线条以指示它们是否存在。

    2. 指定区域在结构的成员中是客户端控制的还是编辑器控制的 `dwBehavior` <xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion> 。 智能大纲显示实现可以混合使用编辑器和客户端控制的大纲和隐藏的文本区域。
