---
title: “消息属性”对话框 | Microsoft Docs
description: 除消息视图中显示的信息外，请查看“消息属性”了解有关消息的更多信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message options
- message options, General
ms.assetid: 58e9dc24-baf6-4ab8-916c-aea28b72e3b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f58ad7344c7de9a9486fcb3ccefbf263688926f
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903059"
---
# <a name="message-properties-dialog-box"></a>“消息属性”对话框
使用此对话框可详细了解特定消息。 若要显示此对话框，请将焦点移至[消息视图](../debugger/messages-view.md)窗口。 在树中选择任意消息节点，然后从“视图”菜单选择“属性” 。

 “常规”选项卡是显示的唯一选项卡。 提供了下列设置：

 **窗口句柄** 此窗口的唯一 ID。 窗口句柄号是重复使用的；它们仅在该窗口的生存期内标识窗口。 单击此值可查看此窗口的属性。

 **嵌套级别** 此消息嵌套的深度，其中 0 表示没有嵌套。

 **消息** 所选窗口消息的编号、状态和名称。

 **lResult** lResult 参数的值（如果有）。

 **wParam** wParam 参数的值（如果有）。

 **lParam** lParam 参数的值（如果有）。 如果此值是指向字符串或结构的指针，则对其进行解码。

## <a name="related-sections"></a>相关章节
 [“消息选项”对话框](../debugger/message-options-dialog-box.md) 用于选择在活动消息视图中列出的消息。

 [“消息搜索”对话框](../debugger/message-search-dialog-box.md) 用于在消息视图中查找特定消息的节点。

 [Spy++ 参考](../debugger/spy-increment-reference.md) 包括介绍每个 Spy++ 菜单和对话框的章节。

 [从“查找窗口”打开消息视图](../debugger/how-to-open-messages-view-from-find-window.md) 介绍如何从“查找窗口”对话框打开消息视图。

 [在消息视图中搜索消息](../debugger/how-to-search-for-a-message-in-messages-view.md) 介绍如何在消息视图中查找特定消息。

 [消息视图](../debugger/messages-view.md) 显示与窗口、进程或线程关联的消息流。

 [Spy++ 视图](../debugger/spy-increment-views.md) 介绍窗口、消息、进程和线程的 Spy++ 树状视图。

 [使用 Spy++](../debugger/using-spy-increment.md) 介绍 Spy++ 工具，并说明其使用方式。