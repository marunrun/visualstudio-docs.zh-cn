---
title: 如何：为编辑器提供上下文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - provide context
ms.assetid: 12df4d06-df6b-4eaf-a7bf-c83655a0c683
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 11a98599a9812cd00650d113170ff55c01ac44db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840502"
---
# <a name="how-to-provide-context-for-editors"></a>如何：为编辑器提供上下文
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

对于编辑器，上下文仅在编辑器具有焦点时，或在将焦点移到工具窗口之前处于活动状态时才处于活动状态。 可以通过执行以下操作为编辑器提供上下文：  
  
1. 创建上下文包。  
  
2. 将上下文包发布到选择元素标识符 (SEID) 。  
  
3. 维护包中的上下文。  
  
   以下过程涵盖了这些任务。 有关提供上下文的详细信息，请参阅本主题后面的 **强健编程** 。  
  
### <a name="to-create-a-context-bag-for-an-editor-or-a-designer"></a>为编辑器或设计器创建上下文包  
  
1. `QueryService`在你 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 的服务上调用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> 。  
  
     返回指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext.CreateEmptyContext%2A> 方法以创建新上下文或子上下文包。  
  
     返回指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext> 。  
  
3. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A> 方法以向上下文或子上下文包添加特性、查找关键字或 F1 关键字。  
  
4. 如果要创建一个子上下文包，请调用方法，将子 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddSubcontext%2A> 上下文包链接到父上下文包。  
  
5. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A> 以在 **动态帮助** 窗口即将更新时接收通知。  
  
     当 " **动态帮助** " 窗口已准备好进行更新时，它会调用你的编辑器，以便在更新发生之前延迟更改上下文。 这样做可以提高性能，因为这样可以延迟运行时间较长的算法，直到系统空闲时间可用。  
  
### <a name="to-publish-the-context-bag-to-the-seid"></a>将上下文包发布到 SEID  
  
1. 对 `QueryService` 服务调用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> 以返回指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A> ，指定元素标识符 (`elementid` 参数) 值 SEID_UserContext，以指示要将上下文传递到全局级别。  
  
3. 当编辑器或设计器变为活动状态时，其对象中的值 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> 将传播到全局选择。 只需在每个会话中完成此过程一次，然后将指针存储在调用时创建的全局上下文 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A> 。  
  
### <a name="to-maintain-the-context-bag"></a>维护上下文包  
  
1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext> 以确保 **动态帮助** 窗口在更新前调用编辑器或设计器。  
  
     对于在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A> 创建并实现上下文包后调用的每个上下文包 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate> ，IDE 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> 以通知上下文提供程序将更新上下文包。 在 **动态帮助** 窗口进行更新之前，可以使用此调用更改上下文包和任何子上下文包中的属性和关键字。  
  
2. 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A> 上下文包调用，以指示编辑器或设计器具有新的上下文。  
  
     当 " **动态帮助** " 窗口调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> 来指示它正在更新时，编辑器或设计器可以为该时间的父上下文包和任何子上下文包适当地更新上下文。  
  
    > [!NOTE]
    > `SetDirty` `true` 每当上下文包中添加或删除上下文时，都会自动将标志设置为。 如果标志设置为，则 **动态帮助** 窗口仅对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A> 上下文包调用 `SetDirty` `true` 。 更新后，它将重置为 `false` 。  
  
3. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A> 以将上下文添加到活动上下文集合或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A> 删除上下文。  
  
## <a name="robust-programming"></a>可靠编程  
 如果你正在编写自己的编辑器，则必须完成本主题中的所有三个过程，以便为编辑器提供上下文。  
  
> [!NOTE]
> 若要正确激活编辑器或设计器窗口，并确保正确更新命令路由，必须对组件调用， <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 使其成为焦点窗口。  
  
 SEID 是根据选择更改的属性的集合。 SEID 信息可通过全局选择获得。 全局选择将连接到由接口触发的事件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> ，并列出了 (当前编辑器、当前工具窗口、当前层次结构等) 所选的所有内容。  
  
 对于编辑器和设计器，每次当光标移动到 word 中时，上下文都可以更改，因此不断更新上下文包是低效的。 若要在编辑器或设计器窗口内检测到光标移动时更有效地进行更新，可以调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A> 。 这样做使您可以在空闲时间之前保存上下文更改，而 IDE 的上下文服务将通知发送到 " **动态帮助** " 窗口正在更新的编辑器或设计器。 本主题中的 "维护上下文包" 过程中使用了此方法。  
  
 为编辑器或设计器中的活动提供上下文后，应提供特定的 F1 关键字，以允许用户获取编辑器或设计器本身的帮助。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>
