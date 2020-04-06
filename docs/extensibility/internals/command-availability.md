---
title: 命令可用性 |微软文档
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dca47d9ed9968c101e3b6b859b51c1cd8d7404db
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709700"
---
# <a name="command-availability"></a>命令可用性

可视化工作室上下文确定哪些命令可用。 上下文可能会根据当前项目、当前编辑器、加载的 VS 包以及集成开发环境 （IDE） 的其他方面而变化。

## <a name="command-contexts"></a>命令上下文

以下命令上下文是最常见的：

- IDE：IDE 提供的命令始终可用。

- VSPackage：VS包可以定义何时显示或隐藏命令。

- 项目：项目命令仅显示当前选定的项目。

- 编辑器：一次只能有一个编辑器处于活动状态。 活动编辑器的命令可用。 编辑器与语言服务密切合作。 语言服务必须在关联的编辑器的上下文中处理其命令。

- 文件类型：编辑器可以加载多种类型的文件。 可用命令可能会根据文件类型更改。

- 活动窗口：最后一个活动文档窗口设置密钥绑定的用户界面 （UI） 上下文。 但是，具有类似于内部 Web 浏览器的键绑定表的工具窗口也可以设置 UI 上下文。 对于多选项卡文档窗口（如 HTML 编辑器），每个选项卡都具有不同的命令上下文 GUID。 注册工具窗口后，它始终在 **"视图"** 菜单上可用。

- UI 上下文：UI 上下文由<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>类的值标识，例如，<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>在生成解决方案时或<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>调试器处于活动状态时。 多个 UI 上下文可以同时处于活动状态。

## <a name="define-custom-context-guids"></a>定义自定义上下文 GUID

如果尚未定义适当的命令上下文 GUID，则可以在 VSPackage 中定义一个，然后根据需要将其编程为活动或非活动，以控制命令的可见性：

1. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>方法注册上下文 GUID。

2. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>方法获取上下文 GUID 的状态。

3. 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>方法打开和关闭上下文 GUID。

> [!CAUTION]
> 请确保您的 VS 包不会影响任何现有上下文 GUID，因为其他 VS 包可能依赖于它们。

## <a name="see-also"></a>请参阅

- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [VS包如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
