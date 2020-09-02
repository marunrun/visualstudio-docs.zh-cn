---
title: 在 "属性" 窗口中更新属性值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Properties window, updating property values
- property values, updating in Properties window
ms.assetid: 9358e8c3-b9d2-4fd4-aaab-cf48d1526db4
caps.latest.revision: 9
manager: jillfra
ms.openlocfilehash: 18ecf0a21c5b2d73bdf8e439d25765b6b275cbd9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62434184"
---
# <a name="updating-property-values-in-the-properties-window"></a>在“属性”窗口中更新属性值
有两种方法可以保持“属性” **** 窗口与属性值更改同步。 第一种是调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 接口，从而提供对基本窗口化功能的访问，包括访问和创建由环境提供的工具窗口和文档窗口。 下面的步骤介绍了此同步过程。  
  
## <a name="updating-property-values-using-ivsuishell"></a>使用 IVsUIShell 更新属性值  
  
#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>使用 IVsUIShell 接口更新属性值  
  
1. 任何时候，只要 Vspackage、项目或编辑器需要创建或枚举工具或文档窗口，就调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>（通过 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 服务）。  
  
2. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> 此方法可以保持 " **属性** " 窗口与项目 (的属性更改，或 " **属性** " 窗口要浏览的任何其他选定对象) ，而无需实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 和激发 <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> 事件。  
  
3. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> 分别创建和禁用层次结构事件的客户端通知，而不要求层次结构实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>。  
  
## <a name="updating-property-values-using-iconnection"></a>使用 IConnection 更新属性值  
 第二种保持“属性” **** 窗口与属性值更改同步的方法是，实现可连接对象上的 `IConnection` ，以指示输出接口是否存在。 如果希望本地化属性名，请从 <xref:System.ComponentModel.ICustomTypeDescriptor> 派生对象。 <xref:System.ComponentModel.ICustomTypeDescriptor> 实现可以修改其返回的属性说明符和更改属性名。 若要本地化说明，请创建一个派生自 <xref:System.ComponentModel.DescriptionAttribute> 的属性并重写 Description 属性。  
  
#### <a name="considerations-in-implementing-the-iconnection-interface"></a>实现 IConnection 接口的注意事项  
  
1. `IConnection` 提供对具有 <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> 接口的枚举器子对象的访问权限。 它还提供对所有连接点的子对象的访问权限，每个子对象均实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口。  
  
2. 任何浏览对象都对实现 <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> 事件负责。 **** “属性”窗口通过 `IConnection`为事件集提供建议。  
  
3. 连接点用于控制在其实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> 时允许的连接数（一个还是多个）。 只允许一个接口的连接点可以通过 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> 方法返回 <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>。  
  
4. 客户端可以调用 `IConnection` 接口，以获得对具有 <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> 接口的枚举器子对象的访问权限。 随后可以调用 <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> 接口，从而为每个输出接口 ID (IID) 枚举连接点。  
  
5. 此外，还可以调用 `IConnection` 从而为每个输出 IID 获取对具有 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口的连接点子对象的访问权限。 通过 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口，客户端使用可连接对象和客户端自己的同步启动或终止通知循环。客户端还可以调用 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口，以获取具有接口的枚举器对象， <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> 以枚举它知道的连接。  
  
## <a name="see-also"></a>另请参阅  
 [公告属性窗口选择跟踪](../misc/announcing-property-window-selection-tracking.md)   
 [扩展属性](../extensibility/internals/extending-properties.md)