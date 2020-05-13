---
title: 在旧语言服务中提供隐藏文本支持
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
ms.openlocfilehash: 8a9d5fe85932f87eb68b6b5a0f5868ebbf8f2b5f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707931"
---
# <a name="how-to-provide-hidden-text-support-in-a-legacy-language-service"></a>如何：在旧语言服务中提供隐藏文本支持
除了大纲区域之外，还可以创建隐藏的文本区域。 隐藏文本区域可以是客户端控制或编辑器控制，并用于完全隐藏文本区域。 编辑器将隐藏区域显示为水平线。 例如 HTML 编辑器中的 **"仅脚本"** 视图。

## <a name="to-implement-a-hidden-text-region"></a>实现隐藏文本区域

1. 调用`QueryService`<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>。

     这将返回指向<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>的指针。

2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.GetHiddenTextSession%2A>， 传入给定文本缓冲区的指针。 这将确定缓冲区是否已存在隐藏文本会话。

3. 如果一个已存在，则不需要创建一个指针，并返回指向现有<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>对象的指针。 使用此指针枚举并创建隐藏的文本区域。 否则，调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager.CreateHiddenTextSession%2A>以创建缓冲区的隐藏文本会话。

     返回指向对象的<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>指针。

    > [!NOTE]
    > 调用`CreateHiddenTextSession`时，可以指定隐藏文本客户端（即<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextClient>。 当用户展开或折叠隐藏文本或大纲时，隐藏文本客户端会通知您。

4. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>一次添加一个或多个新大纲区域，在`reHidReg`（<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>） 参数中指定以下信息：

    1. 在`hrtConcealed`<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构`iType`成员中指定 值，以指示您正在创建隐藏区域，而不是大纲区域。

        > [!NOTE]
        > 隐藏区域时，编辑器会自动在隐藏区域周围显示行，以指示其存在。

    2. 指定区域是客户端控制还是`dwBehavior`<xref:Microsoft.VisualStudio.TextManager.Interop.NewHiddenRegion>结构成员中的编辑器控制。 智能大纲实现可以包含编辑器和客户端控制大纲和隐藏文本区域的组合。
