---
title: 查看 DLL 和可执行文件
titleSuffix: Visual Studio Modules window
ms.custom: seodec18
ms.date: 11/04/2018
ms.topic: how-to
f1_keywords:
- vs.debug.modules
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, Modules window
- Modules window
- executable files, displaying while debugging
- debugging [Visual Studio], displaying modules
- DLLs, displaying while debugging
- modules, displaying
ms.assetid: d840fdca-b035-4452-b652-72580c831896
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fa284a44f75503a2890a15981d2b4f9947be2fa
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348673"
---
# <a name="view-dlls-and-executables-in-the-modules-window-c-c-visual-basic-f"></a>在模块窗口中查看 DLL 和可执行文件（C＃、C++、Visual Basic、F＃）

在 Visual Studio 调试期间，“模块”窗口列出并显示有关应用使用的 DLL 和可执行文件（ .exe 文件）的信息。

> [!NOTE]
> “模块”窗口不适用于 SQL 或脚本调试。

## <a name="use-the-modules-window"></a>使用“模块”窗口

若要在调试时打开“模块”窗口，请选择“调试” > “窗口” > “模块”（或按 Ctrl + Alt + U）   。

默认情况下，“模块”窗口按加载顺序对模块进行排序。 若要按任意窗口列排序，请选择列顶部的对应标头。

## <a name="load-symbols"></a>加载符号

“模块”窗口中的“符号状态”列显示哪些模块已加载调试符号。  如果状态为“已跳过加载符号”、“无法找到或打开 PDB 文件”或“包括/排除设置已禁用加载”，则可以手动加载符号。   有关加载和使用符号的详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

**手动加载符号：**

1. 在“模块”窗口中，右键单击未加载符号的模块。

   - 选择“符号加载信息”，获取有关符号未加载的原因的详细信息。

   - 选择“加载符号”以手动加载符号。

1. 如果符号未加载，请选择“符号设置”以打开“选项”对话框，并指定或更改符号加载位置。 

   可以从公共 Microsoft 符号服务器或其他服务器下载符号，也可以从计算机上的文件夹中加载符号。 有关详细信息，请参阅[指定符号位置和加载行为](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior)。

**更改符号加载行为设置：**

1. 在“模块”窗口中右键单击任一模块。

1. 选择“符号设置”。

1. 选择“加载所有符号”，或选择要包括或排除的模块。

1. 选择“确定”。 更改将在下一个调试会话中生效。

更改特定模块的符号加载行为：

1. 在“模块”窗口中右键单击所需模块。

1. 在右键单击菜单中，选择或取消选择“始终自动加载”。 更改将在下一个调试会话中生效。

## <a name="see-also"></a>请参阅
- [中断执行](/previous-versions/visualstudio/visual-studio-2010/7z9se2d8(v=vs.100))
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
- [指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)