---
title: 文档窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 711033a4ad2e782ecbe509595266426d186bed8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708518"
---
# <a name="document-windows"></a>文档窗口
在 Visual Studio 中，*文档窗口*是与多文档接口 （MDI） 窗口关联的框架子窗口。 文档窗口通常用于显示和修改源代码或文本，但它们还可以承载其他功能类型。 文档窗口：

- 可以组织在父 MDI 中的单独水平或垂直选项卡组中，以便可以同时查看多个文件。

- 可以按父 MDI 中的任何顺序停靠。

- 可以自由浮动。

- 按选项卡顺序链接到其他 MDI 窗口。

  在文档窗口选项卡的快捷菜单上可以找到用于分组、停靠和浮动的命令。

  有关可视化工作室中窗口行为的详细信息，请参阅[自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)。

## <a name="document-window-implementation"></a>文档窗口实现
 文档窗口是通过实现编辑器创建的。 该<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口创建文档窗口作为实例化编辑器的一部分。 有关详细信息，请参阅[编辑器中的旧接口](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)。

> [!NOTE]
> 要在窗口中提供前后导航点，请<xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation>实现接口。 文本编辑器使用文本标记来标识文档中的导航点。

## <a name="the-running-document-table"></a>正在运行的文档表
 IDE 使用正在运行的文档表 （RDT） 来跟踪每个文档窗口的状态。 RDT 是通知文档窗口事件的机制，例如关闭解决方案或编辑文件时。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。

## <a name="see-also"></a>请参阅
- [延迟的文档加载](../../extensibility/internals/delayed-document-loading.md)
