---
title: 选择上下文对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7e1a43997d56f8d89f194fb83d20c1f160378873
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187432"
---
# <a name="selection-context-objects"></a>选择上下文对象
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成的开发环境 (IDE) 使用的全局选择上下文对象来确定在 IDE 中应显示的内容。 在 IDE 中的每个窗口可以有其自己选择上下文对象推送到全局选定内容上下文。 当该窗口具有焦点时，IDE 使用一个窗口中的值更新全局选定内容上下文。 有关详细信息，请参阅[向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。  
  
 每个窗口框架或 IDE 中的站点有一个名为服务<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>。 由你放置在窗口框架的 VSPackage 创建的对象必须调用`QueryService`方法以获取一个指向<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>接口。  
  
 框架窗口可以保留其选择上下文信息将在启动时传播到全局选定内容上下文的部分。 此功能非常有用的可能要开始针对空的所选的工具窗口。  
  
 修改 Vspackage 可以监视的全局选择上下文触发器事件。 Vspackage 可以通过实现来执行以下任务`IVsTrackSelectionEx`和<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>接口：  
  
- 更新层次结构中当前处于活动状态的文件。  
  
- 监视器更改为某些类型的元素。 例如，如果你的 VSPackage 使用特殊**属性**窗口中，你可以监视处于活动状态的更改**属性**窗口，然后重新启动你在需要时。  
  
  按以下顺序显示了典型的选定内容跟踪过程。  
  
1. IDE 从新打开的窗口检索选定内容上下文，并将其放入全局选定内容上下文。 如果选定内容上下文使用 HIERARCHY_DONTPROPAGATE 或 SELCONTAINER_DONTPROPAGATE，该信息不会传播到全局上下文。 有关详细信息，请参阅[向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。  
  
2. 通知事件广播到任何请求它们的 VSPackage。  
  
3. VSPackage 作用于它执行活动，例如更新层次结构中，重新激活一款工具，或者其他类似任务接收的事件。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>   
 [在 Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)   
 [所选内容和 IDE 中的货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [项目类型](../../extensibility/internals/project-types.md)
