---
title: 选择上下文对象 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705513"
---
# <a name="selection-context-objects"></a>选择上下文对象
集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]开发环境 （IDE） 使用全局选择上下文对象来确定 IDE 中应显示的内容。 IDE 中的每个窗口都可以将自己的选择上下文对象推送到全局选择上下文。 当窗口具有焦点时，IDE 会使用窗口中的值更新全局选择上下文。 有关详细信息，请参阅[向用户的反馈](../../extensibility/internals/feedback-to-the-user.md)。

 IDE 中的每个窗口框架或站点都有一个称为<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>的服务。 由在窗口帧中设置的 VSPackage 创建的对象必须调用`QueryService`方法以获取指向接口的<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>指针。

 框架窗口可以在启动时防止其选择上下文信息的某些部分传播到全局选择上下文。 此功能对于可能需要从空选择开始的工具窗口很有用。

 修改全局选择上下文将触发 VSPackages 可以监视的事件。 VS包可以通过实现`IVsTrackSelectionEx`和<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>接口执行以下任务：

- 更新层次结构中的当前活动文件。

- 监视对某些类型的元素的更改。 例如，如果您的 VSPackage 使用特殊的**属性**窗口，则可以监视活动**属性**窗口中的更改，并在需要时重新启动。

  以下序列显示了典型的选择跟踪过程。

1. IDE 从新打开的窗口检索选择上下文，并将其放入全局选择上下文中。 如果选择上下文使用HIERARCHY_DONTPROPAGATE或SELCONTAINER_DONTPROPAGATE，则该信息不会传播到全局上下文。 有关详细信息，请参阅[向用户的反馈](../../extensibility/internals/feedback-to-the-user.md)。

2. 通知事件将广播给请求通知的任何 VSPackage。

3. VSPackage 通过执行更新层次结构、重新激活工具或其他类似任务等活动来对它接收的事件执行。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [项目类型](../../extensibility/internals/project-types.md)
