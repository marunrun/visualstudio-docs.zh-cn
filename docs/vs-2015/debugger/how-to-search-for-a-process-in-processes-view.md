---
title: 如何：在进程视图中搜索进程 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Processes view
- processes, searching for
ms.assetid: 7cb97b37-4a95-4f1b-9eee-4910aa9c115b
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e39168e36e9540ec8c5e23a9030d996b81c4097c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840491"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>如何：在进程视图中搜索进程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过使用进程 ID 或模块字符串作为搜索条件，在进程视图中搜索特定进程。 还可以指定搜索的初始方向。 对话框中的字段将显示进程树中所选进程的属性。  
  
### <a name="to-search-for-a-process-in-processes-view"></a>在进程视图中搜索进程  
  
1. 排列窗口，以使 Spy++ 和活动的[进程视图](../debugger/processes-view.md)窗口可见。  
  
2. 从“搜索”菜单中选择“查找进程”  
  
    此时将打开[“进程搜索”对话框](../debugger/process-search-dialog-box.md)。  
  
3. 键入进程 ID 或模块字符串作为搜索条件。  
  
4. 清除任何不想为其指定值的字段。  
  
   > [!TIP]
   > 若要查找模块拥有的所有进程，请清除“进程”框，然后在“模块”框中键入模块名称。 然后使用“查找下一个”继续搜索进程。  
  
5. 选择“向上”或“向下”作为搜索的初始方向。  
  
6. 单击 **“确定”** 。  
  
   如果找到了匹配的进程，它会在**进程视图**窗口中突出显示。
