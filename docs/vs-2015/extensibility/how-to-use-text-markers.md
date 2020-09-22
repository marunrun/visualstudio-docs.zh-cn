---
title: 如何：使用文本标记 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - using text markers
ms.assetid: 76eed51c-eecb-4579-823e-13df2f0526b9
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 25c3c4f3a3d9a253b9ec671892d0d44ccf9ca3ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840504"
---
# <a name="how-to-use-text-markers"></a>如何：使用文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以应用文本标记来编辑 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> 对象。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-apply-text-markers"></a>应用文本标记  
  
1. 获取类的实例 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> 。  
  
    > [!NOTE]
    > 核心编辑器会自动将标准文本标记应用于它正在编辑的任何文档，并且无需显式应用标准文本标记。  
  
2. 通过 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager.GetRegisteredMarkerTypeID%2A> 使用 `GUID` 要使用的文本标记的来调用方法，获取感兴趣的标记的标记类型 ID。  
  
    > [!NOTE]
    > 不要使用 `GUID` 提供文本标记的 VSPackage 或服务的。  
  
3. 使用通过调用方法获取的标记类型 ID <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager.GetRegisteredMarkerTypeID%2A> 作为参数调用方法，或使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> 方法将文本标记应用于给定的文本区域。  
  
#### <a name="to-add-features-to-text-markers"></a>向文本标记添加功能  
  
1. 可能需要将其他功能添加到文本标记中，如工具提示、特殊的上下文菜单或用于特殊情况的处理程序。 为此，请执行以下操作：  
  
2. 创建实现接口的对象 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 。  
  
3. 如果需要其他功能，请 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced> 在实现接口的同一对象上实现和接口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 。  
  
4. 将 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 您创建的接口传递到对方法的调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> 或 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> 用于将文本标记应用于给定文本区域的方法。  
  
5. 向文本标记区域添加上下文菜单支持时，需要创建菜单。  
  
     有关如何创建上下文菜单的详细信息，请参阅 [上下文](../extensibility/context-menus.md)菜单。  
  
6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]环境根据需要调用提供的接口的方法（如 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetTipText%2A> 方法）或 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A> 方法。  
  
## <a name="see-also"></a>另请参阅  
 [将文本标记与旧版 API 一起使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)   
 [如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)   
 [如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)
