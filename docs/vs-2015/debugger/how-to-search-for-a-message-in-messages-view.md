---
title: 如何：消息在消息视图中搜索 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Message Search dialog box
- Messages view
- messages, searching for
ms.assetid: 732b7ccc-54ea-41db-823b-2b96e3e4083e
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6c89a763389abe364fe70166e63b41f932581837
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430910"
---
# <a name="how-to-search-for-a-message-in-messages-view"></a>如何：在消息视图中搜索消息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将其句柄、 类型或消息 ID 用作搜索条件来搜索特定的消息在消息视图中。 其中的任何一 — 或组合 — 将是有效的搜索条件。 此外可以指定搜索的初始传递方向。 在对话框中的字段是预先加载了当前所选消息的属性。  
  
### <a name="to-search-for-a-message-in-messages-view"></a>若要搜索在消息视图中的消息  
  
1. 排列窗口，因此该 Spy + + 和活动[消息视图](../debugger/messages-view.md)是可见的窗口。  
  
2. 从**搜索**菜单中，选择**查找消息**。  
  
    [消息搜索对话框](../debugger/message-search-dialog-box.md)随即打开。  
  
3. 拖动**查找程序工具**转移所需的窗口。 拖动该工具中，**消息搜索**对话框显示有关所选的窗口的详细信息。  
  
    - 或 -  
  
    如果有你想要检查其消息的窗口的句柄，则键入到**处理**文本框。  
  
    - 或 -  
  
    如果您知道消息类型和/或所需的消息 ID，将其从选定**类型**并**消息**下拉列表菜单，然后清除**处理**文本框。  
  
4. 清除不想为其指定值的任何字段。  
  
   > [!TIP]
   > 若要减少屏幕混乱，请选择**隐藏 Spy**选项。 此选项将隐藏主 Spy + + 窗口中，并仅留下**查找窗口**对话框显示在其他应用程序的前面。 Spy + + 主窗口将还原时，单击**确定**或**取消**，或如果清除**隐藏 Spy + +** 选项。  
  
5. 选择**向上**或**向下**搜索的初始方向。  
  
6. 单击 **“确定”**。  
  
   如果找到匹配的消息时，它将突出显示在消息视图窗口中。 请参阅[消息视图](../debugger/messages-view.md)。
