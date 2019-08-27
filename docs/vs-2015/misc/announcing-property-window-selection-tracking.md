---
title: 宣布属性窗口选定内容跟踪 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63002450"
---
# <a name="announcing-property-window-selection-tracking"></a>宣布属性窗口选定内容跟踪
如果你想要使用**属性**窗口或**属性**页面，例如，窗体、 文本或选择为其想要查看属性，则您必须完成深层次的了解你协调所选内容。 例如，您必须知道是否有单选或多个选择。 然后，你需要地宣布与 IDE 使用你所选内容类型 （单个或多个）<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>接口。 此接口提供所需的信息**属性**窗口。  
  
### <a name="to-announce-selection-to-the-environment"></a>若要宣布对环境的选择  
  
1. 调用`QueryInterface`为<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>。  
  
    1. 若要执行此操作，使用创建时为其传递给视图的站点指针。  
  
    2. 调用`QueryService`的视图从`SID_STrackSelection`服务。  
  
         这将返回一个指向<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>方法每次更改你的选择，并传递一个指针实现的对象到<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>。  
  
     选择容器对象可以使用单个或多个选择，并包含中的所选内容信息`IDispatch`对象。 调用<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>方法通知**属性**所选内容已更改的窗口。 **属性**窗口随后对使用对象<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>以确定是否已发生一个或多个选择，并且实际对象选择的是。  
  
     如果指定多个选择，然后**属性**窗口查找常见属性的对象之间的交集。 如果指定单个对象选择，然后**属性**窗口将显示所有的一个对象的属性。  
  
## <a name="see-also"></a>请参阅  
 [扩展属性](../extensibility/internals/extending-properties.md)   
 [属性页](../extensibility/internals/property-pages.md)