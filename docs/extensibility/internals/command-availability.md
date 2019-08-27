---
title: 命令可用性 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5087e5f7958f9abe46e0caeb2eb03e21285e4da7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338593"
---
# <a name="command-availability"></a>命令可用性

Visual Studio 上下文确定有哪些命令。 根据当前的项目、 当前编辑器、 已加载，Vspackage 和集成的开发环境 (IDE) 的其他方面，上下文可以更改。

## <a name="command-contexts"></a>命令上下文

以下命令上下文是最常见的：

- IDE:提供 IDE 的命令将始终可用。

- VSPackage:Vspackage 可以定义命令时要显示或隐藏。

- 项目：项目命令只显示当前选定的项目。

- 编辑器：一次，只有一个编辑器可以处于活动状态。 可在活动编辑器中的命令。 编辑器与语言服务紧密合作。 语言服务必须处理其关联编辑器的上下文中的命令。

- 文件类型：编辑器可以加载多个文件的类型。 根据文件类型可以更改可用命令。

- 活动窗口：最后一个活动文档窗口设置键绑定的用户界面 (UI) 上下文。 但是，具有类似于内部 web 浏览器的键绑定表的工具窗口还可以设置 UI 上下文。 对于多选项卡式文档窗口，如 HTML 编辑器，每个选项卡具有不同的命令上下文的 GUID。 注册工具窗口后，将始终上可用**视图**菜单。

- UI 上下文：值由标识 UI 上下文<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>类，例如，<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>生成该解决方案后，或<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>调试器处于活动状态时。 多个 UI 上下文可以同时处于活动状态。

## <a name="define-custom-context-guids"></a>定义自定义上下文 Guid

如果尚未定义 GUID 不适当的命令上下文中，可以定义一个在你的 VSPackage 中，然后编写它是活动或非活动所需控制命令的可见性：

1. 通过调用注册上下文 Guid<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>方法。

2. 通过调用获取的 GUID 的上下文状态<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>方法。

3. 将通过调用上下文 Guid 打开和关闭<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>方法。

> [!CAUTION]
> 请确保你的 VSPackage 不因为其他 Vspackage 可能依赖于这些影响任何现有上下文的 Guid。

## <a name="see-also"></a>请参阅

- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)