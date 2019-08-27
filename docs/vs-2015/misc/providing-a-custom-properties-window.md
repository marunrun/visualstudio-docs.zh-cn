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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810692"
---
# <a name="providing-a-custom-properties-window"></a>提供自定义属性窗口
可以提供你自己**属性**对于给定的项目系统，而不是扩展窗口**属性**窗口中提供的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成的开发环境 (IDE)。 最经常遇到的情况是您自己实现放置在窗口框架中的对象。  
  
 如果你未实现对象放置在该窗口框架，但仍有权访问它的其他方式，有多种方法来访问<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>接口，如在此页上的最后一个过程中列出。  
  
### <a name="to-provide-your-properties-window"></a>若要提供在属性窗口  
  
1. 定义一个 GUID，表示你**属性**窗口的实现。  
  
2. 在你<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>实现中，使用<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>服务，以提供您**属性**作为到 Visual Studio 环境服务窗口。  
  
### <a name="to-call-your-properties-window"></a>若要调用在属性窗口  
  
1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A> 方法。  
  
2. `QueryService` 有关<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>从<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>传递到<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A>方法。  
  
3. 获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>从<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>服务。  
  
4. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>第一个参数设置为`SEID_PropertyBrowserSID`(来自<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>枚举)，并使用第三个参数`varValue`，表示字符串形式表示的 guid 你**属性**窗口。 在第一个创建进行此调用一次你**属性**窗口文档窗口。 在调用后这**属性**窗口是窗口框架与相关联。  
  
### <a name="to-obtain-the-window-frame-object-when-you-are-not-the-implementer"></a>若要获取窗口框架对象，当你不是实施者  
  
- 你可以`QueryService`有关<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>服务从<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>与参数`propid`设置为<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>。  
  
- 你可以通过调用获取活动文档窗口<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A>通过 SVsMonitorSelection 服务。 将参数设置`elementid`到`SEID_WindowFrame`取自<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>枚举。  
  
## <a name="see-also"></a>请参阅  
 [扩展属性](../extensibility/internals/extending-properties.md)   
 [属性窗口字段和界面](../extensibility/internals/properties-window-fields-and-interfaces.md)