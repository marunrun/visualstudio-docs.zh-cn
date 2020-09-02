---
title: 提供自定义属性窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- property browsers, providing
- Properties window, providing your own
ms.assetid: 408dcdef-8ef9-4644-97d2-f311cd35824f
caps.latest.revision: 12
manager: jillfra
ms.openlocfilehash: a244463832ff5620efa74a2c7fd20d6d47d79e76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62810692"
---
# <a name="providing-a-custom-properties-window"></a>提供自定义属性窗口
可以为给定的项目系统提供自己的 **属性** 窗口，而不是扩展集成开发环境提供的 " **属性** " 窗口 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (IDE) 。 最常见的情况是，当你自行实现窗口框架中的对象时。  
  
 如果您未实现处于窗口框架中的对象，但仍有一些其他方法对其进行访问，则可以通过多种方式访问 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 此页上最后一个过程中列出的接口。  
  
### <a name="to-provide-your-properties-window"></a>提供属性窗口  
  
1. 定义一个表示 " **属性** " 窗口实现的 GUID。  
  
2. 在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 实现中，使用服务将 " <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> **属性** " 窗口作为服务提供到 Visual Studio 环境。  
  
### <a name="to-call-your-properties-window"></a>调用 "属性" 窗口  
  
1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A> 方法。  
  
2. `QueryService` 对于 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 传入 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A> 方法的。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>从服务中获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> 。  
  
4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>将第一个参数设置为 `SEID_PropertyBrowserSID` 从 <xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID> 枚举) 中获取 (，并使用第三个参数（ `varValue` 表示表示 "**属性**" 窗口的 GUID 的字符串形式）。 第一次创建 " **属性** " 窗口文档窗口时，只需调用一次。 调用后，此 **属性** 窗口将与窗口框架相关联。  
  
### <a name="to-obtain-the-window-frame-object-when-you-are-not-the-implementer"></a>如果不是实施者，则获取窗口框架对象  
  
- 对于的 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> 服务，可以 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> `propid` 将参数设置为 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> 。  
  
- 可以通过调用 SVsMonitorSelection 服务来获取活动文档窗口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> 。 将参数设置 `elementid` 为 `SEID_WindowFrame` ，从枚举中获取 <xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID> 。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../extensibility/internals/extending-properties.md)   
 [Properties Window Fields and Interfaces](../extensibility/internals/properties-window-fields-and-interfaces.md)