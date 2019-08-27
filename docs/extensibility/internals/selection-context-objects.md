---
title: 选择上下文对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef76f417fe2b4371c73d78bbb90b0bd48470746a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318630"
---
# <a name="selection-context-objects"></a>选择上下文对象
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE) 使用的全局选择上下文对象来确定在 IDE 中应显示的内容。 在 IDE 中的每个窗口可以有其自己选择上下文对象推送到全局选定内容上下文。 当该窗口具有焦点时，IDE 使用一个窗口中的值更新全局选定内容上下文。 有关详细信息，请参阅[向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。

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
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [项目类型](../../extensibility/internals/project-types.md)