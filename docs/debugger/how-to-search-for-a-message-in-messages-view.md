---
title: 如何：在消息视图中搜索消息 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Message Search dialog box
- Messages view
- messages, searching for
ms.assetid: 732b7ccc-54ea-41db-823b-2b96e3e4083e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37f99c30c23461ada406bb0650f86d45d2a4a2e9
ms.sourcegitcommit: 3fe6bed9ef8fb1478106645f655c7472009ae43a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64832459"
---
# <a name="how-to-search-for-a-message-in-messages-view"></a>如何：在消息视图中搜索消息
可以使用消息的句柄、类型或消息 ID 作为搜索条件，在消息视图中搜索特定消息。 其中的任何一项（或组合）都是有效的搜索条件。 还可以指定搜索的初始方向。 对话框中的字段预加载了当前所选消息的属性。

### <a name="to-search-for-a-message-in-messages-view"></a>在消息视图中搜索消息

1. 排列窗口，以使 Spy++ 和活动“[消息视图](../debugger/messages-view.md)”窗口可见。

2. 在“搜索”菜单中选择“查找消息” 。

    打开[“消息搜索”对话框](../debugger/message-search-dialog-box.md)。

3. 将“查找程序工具”拖到所需窗口。 拖动该工具时，“消息搜索”对话框将显示所选窗口的详细信息。

   - 或 -

     如果具有要检查其消息的窗口的句柄，请将其键入到“句柄”文本框中。

   - 或 -

     如果知道所需的消息类型和/或消息 ID，请从“类型”和“消息”下拉菜单中选择，并清除“句柄”文本框  。

4. 清除任何不想为其指定值的字段。

   > [!TIP]
   > 若要减少屏幕干扰，请选择“隐藏 Spy”选项。 此选项会隐藏 Spy++ 主窗口，但“查找窗口”对话框仍显示在其他应用程序的前面。 单击“确定”或“取消”时，或清除“隐藏 Spy++”选项时，将还原 Spy++ 主窗口  。

5. 选择“向上”或“向下”作为搜索的初始方向。

6. 单击 **“确定”** 。

   如果找到匹配的消息，它将在“消息视图”窗口中突出显示。 请参阅[消息视图](../debugger/messages-view.md)。