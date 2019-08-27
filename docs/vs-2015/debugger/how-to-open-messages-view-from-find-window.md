---
title: 如何：从查找窗口打开消息视图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Messages View in Spy++, opening
- opening Messages View in Spy++
ms.assetid: 601a193e-432a-417b-9406-6fec9e401264
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ee29135e659eff7e4965b6b1fb0d24de2c2e90cc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157875"
---
# <a name="how-to-open-messages-view-from-find-window"></a>如何：从“查找”窗口打开消息视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可能会发现使用方便**查找窗口**对话框以选择目标窗口中，然后打开该窗口的消息视图。  
  
### <a name="to-open-a-messages-view-window-using-the-find-window-dialog-box"></a>若要打开消息视图窗口使用查找窗口对话框  
  
1. 排列窗口，以便 Spy + + 和目标窗口中可见。  
  
2. 从**Spy**菜单中，选择**查找窗口**。  
  
     [查找窗口对话框](../debugger/find-window-dialog-box.md)随即打开。  
  
3. 从**Windows**选项卡上，拖动**查找程序工具**通过目标窗口。 拖动该工具中，**查找窗口**对话框显示有关所选的窗口的详细信息。  
  
     \- 或 -  
  
     如果有你想要检查 （例如，复制从调试器） 窗口的句柄，则可以键入其**处理**文本框。  
  
4. 下**显示**，选择**消息**。  
  
5. 按“确定”  。  
  
     空白[消息视图](../debugger/messages-view.md)窗口将打开，和一个**消息**菜单添加到 Spy + + 工具栏。  
  
6. 从**消息**菜单中，选择**日志记录选项**。  
  
     [消息选项对话框](../debugger/message-options-dialog-box.md)随即打开。  
  
7. 选择你想要显示的消息的选项。  
  
8. 按**确定**开始日志记录消息。  
  
     根据所选的选项，消息开始流式传送到活动的消息视图窗口。  
  
9. 在必须足够多的消息，请选择**停止日志记录**从**消息**菜单。
