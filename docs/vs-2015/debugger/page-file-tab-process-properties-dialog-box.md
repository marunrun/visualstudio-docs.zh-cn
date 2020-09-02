---
title: “进程属性”对话框 ->“页文件”选项卡 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: daf41a06-8a55-48f6-95f5-49a8416bd308
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 24fdba37be2373623d94f03e45dc5e8a41a74b84
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192719"
---
# <a name="page-file-tab-process-properties-dialog-box"></a>“进程属性”对话框 ->“页文件”选项卡
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用“页文件”选项卡检查进程的页文件。 若要显示[“进程属性”对话框](../debugger/process-properties-dialog-box.md)，请将焦点移动到[进程视图](../debugger/processes-view.md)窗口。 在树中选择任意进程节点，然后从“视图”菜单选择“属性” 。  
  
 “页文件”选项卡中有以下可用设置：  
  
|条目|描述|  
|-----------|-----------------|  
|**页文件字节数**|此进程在页文件中使用的当前页数。 页文件存储进程使用，但不包含在其他文件中的数据页。 所有进程都使用页文件，所以页文件中的空间不足会导致其他进程运行时出现错误。|  
|**峰值页文件字节数**|此进程在页文件中使用的最大页数。|  
|**页面错误**|此进程中执行的线程导致的页面错误数。 如果线程引用的虚拟内存页面不在其主内存内的工作集中，则会发生页面故障。 因此，如果页面在待机列表中并且因此也已经在主内存中，或者页面被共享页面的另一个进程使用，则可能不会从磁盘中检索页面。|
