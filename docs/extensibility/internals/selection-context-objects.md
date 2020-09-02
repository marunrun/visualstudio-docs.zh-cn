---
title: 选择上下文对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e4f33dd0168a667b8f266ea606cecf0c26d62f1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705513"
---
# <a name="selection-context-objects"></a>选择上下文对象
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 使用全局选择上下文对象来确定应在 IDE 中显示的内容。 IDE 中的每个窗口都可以有自己的选择上下文对象，并将其推送到全局选择上下文。 IDE 使用窗口中的值从窗口中的值更新全局选择上下文。 有关详细信息，请参阅 [向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。

 IDE 中的每个窗口框架或站点都有一个名为的服务 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 。 由你的 VSPackage 创建的、放置在窗口框架中的对象必须调用 `QueryService` 方法以获取指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。

 框架窗口可以在启动时将其部分选择上下文信息传播到全局选择上下文。 此功能对可能必须以空选择开始的工具窗口很有用。

 修改全局选择上下文会触发 Vspackage 可以监视的事件。 Vspackage 可以通过实现和接口执行以下 `IVsTrackSelectionEx` 任务 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> ：

- 更新层次结构中当前活动的文件。

- 监视对某些类型的元素的更改。 例如，如果 VSPackage 使用特殊的 " **属性** " 窗口，则可以在 "活动 **属性** " 窗口中监视更改，并在需要时重新启动。

  下面的序列显示了选择跟踪的典型过程。

1. IDE 从新打开的窗口中检索选择上下文，并将其放入全局选择上下文。 如果选择上下文使用 HIERARCHY_DONTPROPAGATE 或 SELCONTAINER_DONTPROPAGATE，则不会将该信息传播到全局上下文。 有关详细信息，请参阅 [向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。

2. 通知事件将广播到任何请求它们的 VSPackage。

3. VSPackage 通过执行活动（例如更新层次结构、重新激活工具或其他类似任务）来处理它所接收的事件。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [项目类型](../../extensibility/internals/project-types.md)
