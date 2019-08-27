---
title: 如何：搜索在进程视图中进程 |Microsoft Docs
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
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64799498"
---
# <a name="how-to-search-for-a-process-in-processes-view"></a>如何：在进程视图中搜索进程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将其进程 ID 或模块字符串用作搜索条件来搜索特定的进程在进程视图中。 此外可以指定搜索的初始传递方向。 进程树中，在对话框中的字段将显示所选的进程的属性。  
  
### <a name="to-search-for-a-process-in-processes-view"></a>若要在进程视图中的进程搜索  
  
1. 排列窗口，因此该 Spy + + 和活动[进程视图](../debugger/processes-view.md)是可见的窗口。  
  
2. 从**搜索**菜单中，选择**查找进程**  
  
    [进程搜索对话框](../debugger/process-search-dialog-box.md)随即打开。  
  
3. 键入的进程 ID 或模块字符串作为搜索条件。  
  
4. 清除不想为其指定值的任何字段。  
  
   > [!TIP]
   > 若要查找模块拥有的所有进程，请清除**进程**框中，键入中的模块名称**模块**框。 然后，使用**查找下一个**表示不继续搜索的进程。  
  
5. 选择**向上**或**向下**搜索的初始方向。  
  
6. 单击 **“确定”** 。  
  
   如果找到匹配的进程，则它以突出显示**进程视图**窗口。
