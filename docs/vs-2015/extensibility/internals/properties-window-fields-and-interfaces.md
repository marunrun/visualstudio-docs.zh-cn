---
title: 属性窗口字段和界面 |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700827"
---
# <a name="properties-window-fields-and-interfaces"></a>Properties Window Fields and Interfaces
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

选择来确定在显示的信息的模型**属性**窗口基于在 IDE 中具有焦点的窗口。 每个窗口中和中所选的窗口中，对象可以具有其选择上下文对象推送到全局选定内容上下文。 当该窗口具有焦点时，环境使用窗口框架中的值更新全局选定内容上下文。 当焦点更改时，因此执行选定内容上下文。  
  
## <a name="tracking-selection-in-the-ide"></a>跟踪在 IDE 中的选定内容  
 窗口框架或站点，拥有的 IDE，具有一个名为服务<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>。 以下步骤说明如何更改在选择到另一个打开的窗口中更改焦点或选择不同的项目项中的用户所致**解决方案资源管理器**，实现更改中显示的内容**属性**窗口。  
  
1. 你在所选的窗口调用中确定位置的 VSPackage 创建的对象<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>能够<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>调用<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>。  
  
2. 选择容器，提供的所选的窗口中，将创建其自己<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>对象。 当所选内容更改，VSPackage 调用<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>来通知任何侦听器在环境中，包括**属性**窗口中，更改。 它还提供对与新的所选内容相关的层次结构和项信息的访问。  
  
3. 调用<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>并将其传递中的所选层次结构项`VSHPROPID_BrowseObject`参数填充<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>对象。  
  
4. 一个派生自[IDispatch 接口](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)为返回<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>请求的内容项，并在环境包装到<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>（请参阅下一步）。 如果调用失败，环境将第二个调用`IVsHierarchy::GetProperty`，并向其传递所选内容容器<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>提供层次结构项。  
  
    VSPackage 不会创建的项目<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>因为实现它的 VSPackage 的提供环境的窗口 (例如，**解决方案资源管理器**) 构造<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>代表其自身。  
  
5. 环境调用的方法<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>若要获取基于的对象`IDispatch`接口以填写**属性**窗口。  
  
   中的值时**属性**更改窗口时，Vspackage 实现`IVsTrackSelectionEx::OnElementValueChangeEx`和`IVsTrackSelectionEx::OnSelectionChangeEx`要报告给此元素的值的更改。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>或<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>中显示的信息保持**属性**窗口同步的属性值。 有关详细信息，请参阅[属性窗口中更新属性值](../../misc/updating-property-values-in-the-properties-window.md)。  
  
   除了选择其他项目项中**解决方案资源管理器**若要显示与该项相关的属性，还可以选择从使用下拉列表可在上一个窗体或文档窗口中的不同对象**属性**窗口。 有关详细信息，请参阅[属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)。  
  
   你可以更改中显示信息的方式**属性**窗口网格中按字母顺序排列到分类，并且如果可用，您还可以通过单击上的相应按钮来打开所选对象的属性页**属性**窗口。 有关详细信息，请参阅[属性窗口按钮](../../extensibility/internals/properties-window-buttons.md)并[属性页](../../extensibility/internals/property-pages.md)。  
  
   最后，底部**属性**窗口中还包含在所选的字段的说明**属性**窗口网格。 有关详细信息，请参阅[从属性窗口获取字段说明](../../misc/getting-field-descriptions-from-the-properties-window.md)。  
  
## <a name="see-also"></a>请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)
