---
title: “消息属性”对话框 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- message options
- message options, General
ms.assetid: 58e9dc24-baf6-4ab8-916c-aea28b72e3b0
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 672bc439a91f0b49c1d198ea666789a6fdcab07e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198169"
---
# <a name="message-properties-dialog-box"></a>“消息属性”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用此对话框可详细了解特定消息。 若要显示此对话框，请将焦点移至[消息视图](../debugger/messages-view.md)窗口。 在树中选择任意消息节点，然后从“视图”菜单选择“属性” 。  
  
 “常规”选项卡是显示的唯一选项卡。 提供了下列设置：  
  
 **窗口句柄**  
 此窗口的唯一 ID。 窗口句柄号是重复使用的；它们仅在该窗口的生存期内标识窗口。 单击此值可查看此窗口的属性。  
  
 **嵌套级别**  
 此消息的嵌套深度，其中0没有嵌套。  
  
 **消息**  
 所选 windows 消息的编号、状态和名称。  
  
 **lResult**  
 *LResult*参数的值（如果有）。  
  
 **wParam**  
 *WParam*参数的值（如果有）。  
  
 **lParam**  
 *LParam*参数的值（如果有）。 如果此值是指向字符串或结构的指针，则对其进行解码。  
  
## <a name="related-sections"></a>相关章节  
 [“消息选项”对话框](../debugger/message-options-dialog-box.md)  
 用于选择在 "活动消息" 视图中列出的消息。  
  
 [“消息搜索”对话框](../debugger/message-search-dialog-box.md)  
 用于在 "消息" 视图中查找特定消息的节点。  
  
 [Spy++ 参考](../debugger/spy-increment-reference.md)  
 包括介绍每个 Spy + + 菜单和对话框的部分。  
  
 [在 "消息" 视图中搜索消息](../debugger/how-to-search-for-a-message-in-messages-view.md)  
 说明如何在 "消息" 视图中查找特定消息。  
  
 [消息视图](../debugger/messages-view.md)  
 显示与窗口、进程或线程关联的消息流。  
  
 [Spy++ 视图](../debugger/spy-increment-views.md)  
 说明窗口的 Spy + + 树视图、消息、进程和线程。  
  
 [使用 Spy++](../debugger/using-spy-increment.md)  
 介绍 Spy + + 工具，并说明如何使用它。
