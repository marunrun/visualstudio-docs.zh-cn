---
title: "\"属性\" 窗口字段和接口 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b58314d64536ecf33cc5589609ee5524a9352629
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700827"
---
# <a name="properties-window-fields-and-interfaces"></a>Properties Window Fields and Interfaces
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

用于确定在 " **属性** " 窗口中显示哪些信息的选择模型基于 IDE 中具有焦点的窗口。 所选窗口中的每个窗口和对象都可以将其选择上下文对象推送到全局选择上下文。 当窗口具有焦点时，环境将使用窗口框架中的值更新全局选择上下文。 焦点发生变化时，选择上下文。  
  
## <a name="tracking-selection-in-the-ide"></a>在 IDE 中跟踪选定内容  
 IDE 拥有的窗口框架或站点具有一个名为的服务 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 。 下面的步骤演示了选择如何更改（由用户将焦点更改为其他打开的窗口或在 **解决方案资源管理器**中选择其他项目项），以更改在 " **属性** " 窗口中显示的内容。  
  
1. 由你的 VSPackage 创建的对象，该对象被放置在选定窗口中，并调用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 来调用 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。  
  
2. 选定窗口提供的选择容器将创建其自己的 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 对象。 选择更改时，VSPackage 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 以通知环境中的任何侦听器，包括更改的 " **属性** " 窗口。 它还提供对与新选择相关的层次结构和项信息的访问。  
  
3. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 并向其传递参数中的选定层次结构项将 `VSHPROPID_BrowseObject` 填充 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 对象。  
  
4. 为请求的项返回派生自 [IDispatch 接口](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5) 的对象 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> ，并且环境会将其包装到 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> (查看以下步骤) 。 如果调用失败，环境将进行第二次调用 `IVsHierarchy::GetProperty` ，并向其传递 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 层次结构项提供的选择容器。  
  
    你的项目 VSPackage 不会创建 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ，因为实现它的环境提供的窗口 VSPackage (例如， **解决方案资源管理器**) <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 代表其构造。  
  
5. 环境调用的方法 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 来基于要 `IDispatch` 在 " **属性** " 窗口中填充的接口来获取对象。  
  
   如果更改了 " **属性** " 窗口中的值，vspackage 将实现 `IVsTrackSelectionEx::OnElementValueChangeEx` 并 `IVsTrackSelectionEx::OnSelectionChangeEx` 报告对元素值所做的更改。 然后，环境将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 或 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 以使 " **属性** " 窗口中显示的信息与属性值保持同步。 有关详细信息，请参阅 [在 "属性" 窗口中更新属性值](../../misc/updating-property-values-in-the-properties-window.md)。  
  
   除了在 **解决方案资源管理器** 中选择其他项目项以显示与该项相关的属性，还可以使用 " **属性** " 窗口中可用的下拉列表从窗体或文档窗口中选择其他对象。 有关详细信息，请参阅 [属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)。  
  
   您可以将 " **属性** " 窗口网格中显示的信息从字母更改为分类，如果可用，还可以通过单击 " **属性** " 窗口中的相应按钮，为所选对象打开属性页。 有关详细信息，请参阅 [属性窗口按钮](../../extensibility/internals/properties-window-buttons.md) 和 [属性页](../../extensibility/internals/property-pages.md)。  
  
   最后，" **属性** " 窗口的底部还包含 " **属性** " 窗口网格中所选字段的说明。 有关详细信息，请参阅 ["属性" 窗口中的获取字段说明](../../misc/getting-field-descriptions-from-the-properties-window.md)。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)
