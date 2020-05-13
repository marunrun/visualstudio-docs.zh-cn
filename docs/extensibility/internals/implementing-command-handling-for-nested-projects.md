---
title: 为嵌套项目实施命令处理 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2092fc8033d5a5cc53b12bd63a945bd9865ca30e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707599"
---
# <a name="implementing-command-handling-for-nested-projects"></a>实现嵌套项目的命令处理
IDE 可以将通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>和<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口传递到嵌套项目的命令，或者父项目可以筛选或重写命令。

> [!NOTE]
> 只能筛选父项目通常处理的命令。 无法筛选 IDE 处理的**生成**和**部署**等命令。

 以下步骤描述了实现命令处理的过程。

## <a name="procedures"></a>过程

#### <a name="to-implement-command-handling"></a>实现命令处理

1. 当用户选择嵌套项目中的嵌套项目或节点时：

   1. IDE 调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法。

      — 或者 —

   2. 如果命令源自层次结构窗口（如解决方案资源管理器中的快捷菜单命令），则 IDE 将在项目的父窗口中<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>调用该方法。

2. 父项目可以检查要传递给`QueryStatus`的参数，如`pguidCmdGroup`和`prgCmds`，以确定父项目是否应筛选命令。 如果父项目实现以筛选命令，则应设置：

   ```
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;
   // make sure it is disabled
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;
   ```

    然后父项目应返回`S_OK`。

    如果父项目不筛选命令，则它应仅返回`S_OK`。 在这种情况下，IDE 会自动将命令路由到子项目。

    父项目不必将命令路由到子项目。 IDE 执行此任务。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
