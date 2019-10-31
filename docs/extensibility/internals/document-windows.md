---
title: 文档窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5d29d64090320a8f62491209773145c024564efa
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186621"
---
# <a name="document-windows"></a>文档窗口
在 Visual Studio 中，*文档窗口*是一个与多文档界面（MDI）窗口关联的带边框的子窗口。 文档窗口通常用于显示和修改源代码或文本，但它们也可以承载其他功能类型。 文档窗口：

- 可以在父 MDI 的单独的水平或垂直选项卡组中进行组织，以便可以同时查看多个文件。

- 可按任何顺序停靠在父 MDI 中。

- 可以自由浮动。

- 按 tab 键顺序链接到其他 MDI 窗口。

  可在文档窗口选项卡的快捷菜单上找到用于分组、停靠和浮动的命令。

  有关 Visual Studio 中窗口行为的详细信息，请参阅[自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)。

## <a name="document-window-implementation"></a>文档窗口实现
 文档窗口是通过实现编辑器创建的。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 接口在实例化编辑器时创建文档窗口。 有关详细信息，请参阅[编辑器中的旧接口](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)。

> [!NOTE]
> 若要在窗口中提供向后和向前导航点，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> 接口。 文本编辑器使用文本标记来标识文档中的导航点。

## <a name="the-running-document-table"></a>正在运行的文档表
 IDE 使用正在运行的文档表（RDT）来跟踪每个文档窗口的状态。 RDT 是一种机制，通过该机制可以通知文档窗口事件，例如关闭解决方案或编辑文件时。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。

## <a name="see-also"></a>请参阅
- [延迟的文档加载](../../extensibility/internals/delayed-document-loading.md)