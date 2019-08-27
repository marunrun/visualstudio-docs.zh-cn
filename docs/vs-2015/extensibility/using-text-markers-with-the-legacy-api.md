---
title: 旧版 API 中使用文本标记 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text markers
ms.assetid: 937a0b19-1216-45d5-a7ad-4fe1d6f73097
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3dff5e6ecf60d389730841e99b87db584465e020
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695482"
---
# <a name="using-text-markers-with-the-legacy-api"></a>旧版 API 中使用文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本标记是区域的文本的浮动的范围内的缓冲区中，可能会影响显示和文本的行为。 标记包括断点、 书签、 波浪形下划线和只读区域。 文本标记为基本上不同于语法颜色设置。 语法颜色设置是通信与文本的区域关联的语言语法的快速方法。 Windows 重新绘制屏幕时速度很重要时通常所请求语法颜色设置。 语法颜色设置更改文本的颜色。 文本标记可以更改许多其他文本属性。 文本标记可以"浮动"并将应用特殊行为和颜色设置。  
  
 由于与文本标记相关的性能开销，而不要创建多个标记的文本缓冲区。 每个标记是用户编辑缓冲区内容每次更新。  
  
> [!NOTE]
> 用户可以更改可见标记类型，但不是其形状和样式的颜色。 有关详细信息，请参阅[字体和 Colors，Environment，Options Dialog Box](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|说明|  
|-----------|-----------------|  
|[如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)|描述如何添加由提供的标准文本标记类型[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器文本视图。|  
|[如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)|介绍如何实现的实例[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]标记，用于通过使用红色的波浪形下划线指示错误。|  
|[如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)|介绍如何创建和自定义文本标记类型添加到文本视图。|  
|[如何：使用文本标记](../extensibility/how-to-use-text-markers.md)|介绍如何添加文本标记。|  
|[核心编辑器内](../extensibility/inside-the-core-editor.md)|介绍核心编辑器的功能，并提供有关如何自定义核心编辑器的详细信息。|  
|[编辑器功能](https://msdn.microsoft.com/bdac940d-1f14-4019-a01f-fd0bb3dc7198)|描述中提供的功能[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]核心编辑器。|  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>  
 提供了统一的预定义的由编辑器还是由 VSPackage 注册获取有关特定文本标记类型的信息的机制。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLineMarker>  
 提供对访问和使用二维坐标，调整文本标记的文本缓冲区中的位置。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>  
 提供用于管理文本标记的方法。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>  
 提供对回调[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]IDE 和其他进程，用于调整文本标记。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced>  
 扩展了可通过功能<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>通过提供其他回调接口。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>  
 扩展了可通过功能<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>通过提供其他回调接口。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerColorSet>  
 启用标记类型以确定其他标记类型是否共享相同的颜色集。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>  
 提供核心编辑器中的文本标记的上下文。 对于每个核心编辑器中的文本标记类型，则 IDE 将创建一个单独<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>对象。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerGlyphDropHandler>  
 提供标记标志符号支持拖放编辑处理程序。 标志符号是一个图标，指示标记的位置。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>  
 返回<xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>接口从服务提供到其他 Vspackage 的标记的文本。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamMarker>  
 提供对访问和使用一维的坐标调整文本标记的文本缓冲区中的位置。 如果可能，不要使用此接口。
