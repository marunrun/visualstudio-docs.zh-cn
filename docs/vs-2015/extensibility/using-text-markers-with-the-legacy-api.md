---
title: 将文本标记与旧版 API 一起使用 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695482"
---
# <a name="using-text-markers-with-the-legacy-api"></a>对旧版 API 使用文本标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本标记是缓冲区中的浮动文本范围，可以影响文本区域的显示和行为。 标记包括断点、书签、波浪下划线和只读区域。 文本标记基本不同于语法着色。 语法着色是一种用于传达与文本区域关联的语言语法的快速方法。 通常，在 Windows 重画屏幕时，通常会请求语法着色，因为速度非常重要。 语法着色仅更改文本的颜色。 文本标记可以更改许多其他文本属性。 文本标记可以 "浮动" 并应用特殊行为和着色。  
  
 由于与文本标记相关联的性能开销，因此不要为文本缓冲区创建许多标记。 每次用户编辑缓冲区内容时，都会更新每个标记。  
  
> [!NOTE]
> 用户可以更改可见标记类型的颜色，但不能更改其形状和样式。 有关详细信息，请参阅 " [字体和颜色、环境、选项" 对话框](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|说明|  
|-----------|-----------------|  
|[如何：添加标准文本标记](../extensibility/how-to-add-standard-text-markers.md)|介绍如何将核心编辑器提供的标准文本标记类型添加 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 到文本视图。|  
|[如何：实现错误标记](../extensibility/how-to-implement-error-markers.md)|描述如何实现 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 用于通过使用红色波浪下划线指示错误的标记的实例。|  
|[如何：创建自定义文本标记](../extensibility/how-to-create-custom-text-markers.md)|介绍如何创建自定义文本标记类型并将其添加到文本视图。|  
|[如何：使用文本标记](../extensibility/how-to-use-text-markers.md)|说明如何添加文本标记。|  
|[核心编辑器内](../extensibility/inside-the-core-editor.md)|介绍核心编辑器的功能，并提供有关如何自定义核心编辑器的详细信息。|  
|[编辑器功能](https://msdn.microsoft.com/bdac940d-1f14-4019-a01f-fd0bb3dc7198)|描述核心编辑器中可用的功能 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。|  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>  
 提供统一的机制，用于获取特定文本标记类型的信息，无论是由编辑器预定义还是由 VSPackage 注册。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLineMarker>  
 通过使用二维坐标，可以访问和调整文本缓冲区中文本标记的位置。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>  
 提供用于管理文本标记的方法。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>  
 提供对 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 和用于调整文本标记的其他进程的回调。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced>  
 通过提供额外的回调，扩展可通过接口获得的功能 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>  
 通过提供额外的回调，扩展可通过接口获得的功能 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> 。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerColorSet>  
 允许标记类型确定其他标记类型是否共享同一种颜色集。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>  
 在核心编辑器中为文本标记提供上下文。 对于核心编辑器中的每个文本标记类型，IDE 将创建一个单独的 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> 对象。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerGlyphDropHandler>  
 为标记（其标志符号支持拖放编辑）提供的处理程序。 标志符号是一个图标，指示标记的位置。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>从服务返回一个接口，该接口向其他 vspackage 提供文本标记。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamMarker>  
 通过使用一维坐标，可以访问和调整文本缓冲区中文本标记的位置。 如果可能，请不要使用此接口。
