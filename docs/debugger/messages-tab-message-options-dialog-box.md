---
title: 消息选项卡上，消息选项对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message options, Messages
ms.assetid: fb9fa211-e82c-40a5-9e4b-ba8de07313c0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: de50e6fe997ce10266cbb51f2fd91c318ab2bd1f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905523"
---
# <a name="messages-tab-message-options-dialog-box"></a>“消息选项”对话框 ->“消息”选项卡
使用**消息**选项卡以选择列表中的消息类型[消息视图](../debugger/messages-view.md)，并指定消息搜索条件。 若要显示[消息选项对话框](../debugger/message-options-dialog-box.md)，选择**日志消息**从**Spy**菜单。

 通常情况下，首先选择**消息组**，然后通过选择单个微调所选内容**查看的消息**。 **所有**按钮选择所有消息类型，并**None**按钮将清除所有类型。

 以下设置位于**消息**选项卡：

 **查看的消息**选择查看的特定消息。 在创建新的消息窗口时，它可以显示所有消息。 筛选来自消息时**消息**选项卡上，该筛选器仅适用于新消息，不均已显示在 Windows 视图中的消息。

 **消息组**选择消息组进行查看。 可用组包括：

- 使用代码大于或等于 WM_USER WM_USER:

- 注册： 注册**RegisterWindowMessage**调用

- 未知： 范围 0 到 (WM_USER-1) 中的未知的消息

  请注意，这些**消息组**不会映射到下的特定项**查看的消息**。 当选择一个组时，所选内容将直接应用到消息流。

  中的灰色的复选框**消息组**指示**查看的消息**为该组中的消息，已修改列表框中; 不是所有在该组中的消息类型选择。

  **将设置保存为默认**将以供将来使用的当前设置保存为消息搜索选项。 退出 Spy + + 时，还会保存这些设置。