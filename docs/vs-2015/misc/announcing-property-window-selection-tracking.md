---
title: 公告属性窗口选择跟踪 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], property pages support
- property pages, tracking selection
- Properties window, tracking selection
- selection, tracking
- editors [Visual Studio SDK], Properties window support
ms.assetid: a7536f82-afd7-4894-9a60-84307fb92b7e
caps.latest.revision: 13
manager: jillfra
ms.openlocfilehash: 6296993d3a1f5039024556f09b721daa82ca4f53
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "63002450"
---
# <a name="announcing-property-window-selection-tracking"></a>宣布属性窗口选定内容跟踪
如果要使用 " **属性** " 窗口或 " **属性** " 页（例如，要查看其属性的窗体、文本或选定内容），则必须全面了解如何协调选定内容。 例如，你必须知道你是具有单个选择还是多个选择。 然后，需要使用接口将选择类型 (单个或多个) 公告到 IDE <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。 此接口提供 " **属性** " 窗口所需的信息。  
  
### <a name="to-announce-selection-to-the-environment"></a>向环境公布选定内容  
  
1. 调用 `QueryInterface` <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 。  
  
    1. 为此，请在创建视图时使用传递给该视图的站点指针。  
  
    2. `QueryService`从服务的视图中调用 `SID_STrackSelection` 。  
  
         这会返回指向的指针 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>每次选择更改时调用方法，并将指针传递到实现的对象 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 。  
  
     选择容器对象可以使用单个或多个选择，并在对象中包含选择信息 `IDispatch` 。 调用 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 方法会向 " **属性** " 窗口通知所选内容已更改。 然后，" **属性** " 窗口使用上的对象 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 来确定是否发生了单个或多个选择，以及实际选择的对象是什么。  
  
     如果指定多重选择，则 " **属性** " 窗口将查找对象的公共属性之间的交集。 如果指定单个对象选择，则 " **属性** " 窗口将显示一个对象的所有属性。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../extensibility/internals/extending-properties.md)   
 [属性页](../extensibility/internals/property-pages.md)