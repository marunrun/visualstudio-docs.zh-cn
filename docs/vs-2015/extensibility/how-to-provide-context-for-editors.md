---
title: 如何：为编辑器提供的上下文 |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435896"
---
# <a name="how-to-provide-context-for-editors"></a>如何：为编辑器提供的上下文
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器上下文处于活动状态，仅当编辑器具有焦点或立即之前焦点已移动到工具窗口具有焦点时。 可为编辑器提供上下文，通过执行以下操作：  
  
1. 创建上下文包。  
  
2. 将上下文包发布到所选内容元素标识符 (SEID)。  
  
3. 维护包中的上下文。  
  
   以下过程包含在这些任务。 提供上下文的详细信息，请参阅**可靠编程**本主题中更高版本。  
  
### <a name="to-create-a-context-bag-for-an-editor-or-a-designer"></a>为编辑器或设计器创建上下文包  
  
1. 调用`QueryService`上你<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>接口<xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext>服务。  
  
     一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext>接口将返回。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext.CreateEmptyContext%2A>方法来创建一个新的上下文或子上下文包。  
  
     一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext>接口将返回。  
  
3. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>方法将属性、 查找关键字或 F1 关键字添加到上下文或子上下文包。  
  
4. 如果要创建一个子上下文包，则调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddSubcontext%2A>方法以将子上下文包链接到父上下文包。  
  
5. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>若要接收通知时**动态帮助**窗口即将更新。  
  
     无**动态帮助**窗口调用您的编辑器已准备好更新使你能够延迟更改上下文，直到发生更新时。 执行此操作可以提高性能，因为它允许您以后再运行耗时的算法，直到系统空闲时间可用。  
  
### <a name="to-publish-the-context-bag-to-the-seid"></a>若要将上下文包发布到 SEID  
  
1. 调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>服务返回一个指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>接口。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>，指定的元素标识符 (`elementid`参数) SEID_UserContext 以指示要将上下文传递给全局级别的值。  
  
3. 编辑器或设计器变为活动状态时中的值及其<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>对象传播到全局选择。 只需完成一次每个会话，此过程，然后将存储到您在调用时创建的全局上下文指针<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>。  
  
### <a name="to-maintain-the-context-bag"></a>若要维护的上下文包  
  
1. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext>，确保**动态帮助**窗口调用编辑器或设计器之前它将更新。  
  
     已调用每个上下文包<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>上下文包创建，并已实现后<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate>，IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>通知上下文提供程序将更新上下文包。 可以使用此调用之前更改的属性和关键字上下文包中和任何子上下文包，在**动态帮助**窗口更新发生。  
  
2. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>来指示的编辑器或设计器具有新的上下文的上下文包上。  
  
     当**动态帮助**窗口调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>以指示它正在更新，编辑器或设计器可以在该时间更新父上下文包和任何子上下文包适当的上下文。  
  
    > [!NOTE]
    > `SetDirty`标志将自动设置为`true`每当添加或删除从上下文包上下文。 **动态帮助**窗口将仅调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>对上下文包如果`SetDirty`标志设置为`true`。 重置为`false`更新后。  
  
3. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>以将上下文添加到活动的上下文集合或<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A>删除上下文。  
  
## <a name="robust-programming"></a>可靠编程  
 如果你正在编写您自己的编辑器，则必须完成所有这三个本主题为编辑器中提供的上下文中的过程。  
  
> [!NOTE]
> 若要正确激活的编辑器或设计器窗口并确保命令路由已正确更新，必须调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>组件以使其焦点窗口上。  
  
 SEID 是基于对所选内容更改的属性的集合。 可通过全局选择 SEID 信息。 全局选择连接到触发的事件<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>接口，并且已将所有内容的列表选择了 （当前编辑器、 当前工具窗口、 当前层次结构等）。  
  
 编辑器和设计器，在其上下文可以只要更改光标移动在某个词中低效来不断更新上下文包。 若要使更新更高效随时检测光标移动在编辑器或设计器窗口中，可以调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>。 执行此操作，可保存上下文更改，直到没有空闲时间和 IDE 的上下文服务将通知发送到编辑器或设计器的**动态帮助**窗口正在更新。 在"维护上下文包"过程中本主题中使用此方法。  
  
 提供编辑器或设计器中活动的上下文之后, 应提供特定的 F1 关键字，若要允许用户以获取有关编辑器或设计器本身的帮助。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AddAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.AdviseUpdate%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.RemoveAttribute%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.SetDirty%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContextUpdate.UpdateUserContext%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>
