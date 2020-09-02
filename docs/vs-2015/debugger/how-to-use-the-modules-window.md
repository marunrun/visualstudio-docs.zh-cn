---
title: 如何：使用 "模块" 窗口 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696131"
---
# <a name="how-to-use-the-modules-window"></a>如何：使用“模块”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 此功能不可用于 SQL 或脚本调试。  
  
 " **模块** " 窗口列出程序使用的 DLL 和 EXE，并显示每个 DLL 和 EXE 的相关信息。  
  
### <a name="to-display-the-modules-window-in-break-mode-or-in-run-mode"></a>在中断模式或运行模式下显示“模块”窗口  
  
- 在 " **调试** " 菜单上，选择 " **窗口**"，然后单击 " **模块**"。  
  
     默认情况下，“模块”窗口按加载顺序对模块进行排序。 但是，可以选择按任意列来排序。  
  
### <a name="to-sort-by-any-column"></a>按任意列排序  
  
- 单击该列顶部的按钮。  
  
     您可以使用快捷菜单加载符号或指定 " **模块** " 窗口中的符号路径。  
  
## <a name="loading-symbols"></a>加载符号  
 在 " **模块** " 窗口中，可以看到加载了调试符号的模块。 此信息显示在 " **符号状态** " 列中。 如果状态为 "已 **跳过 loadingCannot" 查找或打开 PDB 文件**，或 **通过 "包含/排除" 设置禁用了加载**，则可以定向调试器从 Microsoft 公共符号服务器下载符号，或者从计算机上的符号目录中加载符号。 有关详细信息，请参阅 [指定符号 ( .pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)  
  
#### <a name="to-load-symbols-manually"></a>手动加载符号  
  
1. 在 " **模块** " 窗口中，右键单击尚未加载符号的模块。  
  
2. 指向 " **加载符号** "，然后单击 " **Microsoft 符号服务器** " 或 " **符号路径**"。  
  
#### <a name="to-change-symbol-load-settings"></a>更改符号加载设置  
  
1. 在“模块”窗口中右键单击任一模块。  
  
2. 单击 " **符号设置**"。  
  
     你现在可以更改符号加载设置，如 [指定符号位置和加载行为](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior)中所述。 只有重新启动调试会话，更改才会生效。  
  
#### <a name="to-change-symbol-load-behavior-for-a-specific-module"></a>为特定模块更改符号加载行为  
  
1. 在“模块”窗口中右键单击所需模块。  
  
2. 指向 " **自动符号加载设置** "，然后单击 " **始终手动** 或 **默认**加载"。 只有重新启动调试会话，更改才会生效。  
  
## <a name="see-also"></a>另请参阅  
 [中断执行](https://msdn.microsoft.com/30fc4643-f337-4651-b1ff-f2de2c098d40)   
 [在调试器中查看数据](../debugger/viewing-data-in-the-debugger.md)   
 [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
