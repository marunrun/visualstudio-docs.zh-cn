---
title: 进程视图 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.processesview
helpviewer_keywords:
- Processes view
ms.assetid: e144e70e-eef2-45a7-a562-a177f177d9a1
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d8b9c04d1cabd44418c70725ef331c9c4b5ec67e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580489"
---
# <a name="processes-view"></a>进程视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

进程视图显示系统上所有活动进程的树。 进程 ID 和模块名称会进行显示。 如果要检查特定系统进程（通常对应于正在执行的程序），请使用进程视图。 进程由模块名称标识，或者指定为“系统进程”。  
  
 Microsoft Windows 支持多个进程。 每个进程都可以有一个或多个线程，而每个线程都可以有一个或多个关联的顶级窗口。 每个顶级窗口都可以拥有一系列窗口。 \+ 符号指示级别处于折叠状态。 折叠视图中每个进程占一行。 单击 + 符号可展开级别。  
  
 如果要检查特定系统进程（通常对应于正在执行的程序），请使用进程视图。 进程由模块名称标识，或者指定为“系统进程”。 若要查找进程，请折叠树并搜索列表。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-open-the-processes-view"></a>打开进程视图  
  
1. 从“Spy”菜单中，选择“进程” 。  
  
   ![Spy&#43;&#43; 进程视图](../debugger/media/spy-processes.png "Spy + + _Processes")  
   Spy++ 进程视图  
  
   上图显示了展开了进程和线程节点的进程视图。  
  
### <a name="in-this-section"></a>本节内容  
 [在进程视图中搜索进程](../debugger/how-to-search-for-a-process-in-processes-view.md)  
 说明如何在进程视图中查找特定进程。  
  
 [显示进程属性](../debugger/how-to-display-process-properties.md)  
 说明如何显示消息的详细信息。  
  
### <a name="related-sections"></a>相关章节  
 [Spy++ 视图](../debugger/spy-increment-views.md)  
 说明窗口的 Spy + + 树视图、消息、进程和线程。  
  
 [使用 Spy++](../debugger/using-spy-increment.md)  
 介绍 Spy + + 工具，并说明如何使用它。  
  
 [“进程搜索”对话框](../debugger/process-search-dialog-box.md)  
 用于在进程视图中查找特定进程的节点。  
  
 [“进程属性”对话框](../debugger/process-properties-dialog-box.md)  
 显示在 "进程" 视图中选择的进程的属性。  
  
 [Spy++ 参考](../debugger/spy-increment-reference.md)  
 包括介绍每个 Spy + + 菜单和对话框的部分。
