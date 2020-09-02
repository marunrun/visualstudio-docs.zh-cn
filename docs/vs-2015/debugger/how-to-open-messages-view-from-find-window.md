---
title: 如何：从“查找窗口”打开消息视图 | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157875"
---
# <a name="how-to-open-messages-view-from-find-window"></a>如何：从“查找”窗口打开消息视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可能会发现使用“查找窗口”对话框选择目标窗口，然后打开该窗口的消息视图会十分方便。  
  
### <a name="to-open-a-messages-view-window-using-the-find-window-dialog-box"></a>使用“查找窗口”对话框打开消息视图窗口  
  
1. 排列窗口，使 Spy++ 和目标窗口都可见。  
  
2. 从“Spy”菜单中，选择“查找窗口” 。  
  
     [“查找窗口”对话框](../debugger/find-window-dialog-box.md)打开。  
  
3. 从“窗口”选项卡，将“查找程序工具”拖到目标窗口上。 拖动该工具时，“查找窗口”对话框将显示有关所选窗口的详细信息。  
  
     - 或 -  
  
     如果你有要检查的窗口的句柄（例如，从调试器复制），则可以其键入到“句柄”文本框中。  
  
4. 在“显示”下，选择“消息” 。  
  
5. 按“确定”。  
  
     空白[消息视图](../debugger/messages-view.md)窗口会打开，并且“消息”菜单会添加到 Spy++ 工具栏。  
  
6. 从“消息”菜单中，选择“日志记录选项”。  
  
     [“消息选项”对话框](../debugger/message-options-dialog-box.md)会打开。  
  
7. 为要显示的消息选择选项。  
  
8. 按“确定”以开始记录消息。  
  
     根据所选的选项，消息开始流入活动消息视图窗口中。  
  
9. 有足够消息时，从“消息”菜单中选择“停止记录”。
