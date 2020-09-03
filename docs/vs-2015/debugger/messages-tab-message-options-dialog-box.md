---
title: “消息选项”对话框 ->“消息”选项卡 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- message options, Messages
ms.assetid: fb9fa211-e82c-40a5-9e4b-ba8de07313c0
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a9eb1c88d935fa307e8b86a9a75da423bc08111c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149433"
---
# <a name="messages-tab-message-options-dialog-box"></a>“消息选项”对话框 ->“消息”选项卡
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用“消息”选项卡可选择要在[消息视图](../debugger/messages-view.md)中列出的消息类型，并指定消息搜索条件。 若要显示[“消息选项”对话框](../debugger/message-options-dialog-box.md)，请从 Spy 菜单中选择“日志消息” 。  
  
 通常，首先选择“消息组”，然后通过选择各个“要查看的消息”来微调所选内容。 “全部”按钮将选择所有消息类型，“无”按钮将清除所有类型。  
  
 “消息”选项卡中有以下可用设置：  
  
 **要查看的消息**  
 选择要查看的特定消息。 创建新的“消息”窗口时，它可以显示所有消息。 从“消息”选项卡筛选消息时，该筛选器仅适用于新消息，不适用于窗口视图中已显示的消息。  
  
 **消息组**  
 选择要查看的消息组。 可用的组包括：  
  
- WM_USER：代码大于或等于 WM_USER  
  
- 已注册：已通过 RegisterWindowMessage 调用注册  
  
- 未知：0到 (范围内的未知消息 WM_USER – 1)   
  
  请注意，这些消息组不会映射到“要查看的消息”下的特定条目。 选择某个组时，所选内容将直接应用于消息流。  
  
  “消息组”中的灰色复选框表示已为该组中的消息修改了“要查看的消息”列表框，而不是表示该组中的所有消息类型都处于选中状态。  
  
  **保存为默认设置**  
  保存当前设置以供将来用作消息搜索选项。 退出 Spy++ 时也会保存这些设置。
