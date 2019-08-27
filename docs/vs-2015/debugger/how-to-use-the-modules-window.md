---
title: 如何：使用模块窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.modules
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Modules window
- Modules window
- executable files, displaying while debugging
- debugging [Visual Studio], displaying modules
- DLLs, displaying while debugging
- modules, displaying
ms.assetid: d840fdca-b035-4452-b652-72580c831896
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b592515692e23dce49c125c7895bd158904b653f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696131"
---
# <a name="how-to-use-the-modules-window"></a>如何：使用模块窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 此功能不可用于 SQL 或脚本调试。  
  
 **模块**窗口列出了由您的程序并显示每个相关信息的 Dll 和 EXE。  
  
### <a name="to-display-the-modules-window-in-break-mode-or-in-run-mode"></a>在中断模式或运行模式下显示“模块”窗口  
  
- 上**调试**菜单中，选择**Windows**，然后单击**模块**。  
  
     默认情况下，“模块”窗口按加载顺序对模块进行排序。 但是，可以选择按任意列来排序。  
  
### <a name="to-sort-by-any-column"></a>按任意列排序  
  
- 单击该列顶部的按钮。  
  
     您可以加载符号或指定符号路径**模块**窗口中使用的快捷菜单。  
  
## <a name="loading-symbols"></a>加载符号  
 在中**模块**窗口中，您可以看到哪些模块加载了调试符号。 此信息显示在**符号状态**列。 如果状态显示为**已跳过 loadingCannot 找到或打开 PDB 文件**，或**包括/排除设置已禁用加载**，可以指示调试器从 Microsoft 公共符号下载符号服务器或者从您的计算机上的符号目录加载符号。 有关详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)  
  
#### <a name="to-load-symbols-manually"></a>手动加载符号  
  
1. 在中**模块**窗口中，右击还未加载符号的模块的。  
  
2. 指向**负载从符号**，然后单击**Microsoft 符号服务器**或**符号路径**。  
  
#### <a name="to-change-symbol-load-settings"></a>更改符号加载设置  
  
1. 在“模块”窗口中右键单击任一模块。  
  
2. 单击**符号设置**。  
  
     现在可以更改符号加载设置，如中所述[指定符号位置和加载行为](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior)。 只有重新启动调试会话，更改才会生效。  
  
#### <a name="to-change-symbol-load-behavior-for-a-specific-module"></a>为特定模块更改符号加载行为  
  
1. 在“模块”窗口中右键单击所需模块。  
  
2. 指向**自动符号加载设置**，然后单击**始终手动加载**或**默认**。 只有重新启动调试会话，更改才会生效。  
  
## <a name="see-also"></a>请参阅  
 [中断执行](https://msdn.microsoft.com/30fc4643-f337-4651-b1ff-f2de2c098d40)   
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)   
 [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
