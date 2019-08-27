---
title: 如何：调试插入的代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.injected
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- assembly language, viewing
- debugging [C++], viewing assembly code
- debugging [C++], injected code
- debugging [C++], enabling source annotation
- injected code
- Show Source Code command [debugger]
- debugging [C++], using attributes
- disassembly code, debugging
ms.assetid: a1b4104d-d49e-451f-a91e-e39ceaf35875
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: df35a25534961c6ab94891d2da6fe54f05c37a3e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681092"
---
# <a name="how-to-debug-injected-code"></a>如何：调试插入的代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 使用特性可大大简化 C++ 编程。 有关详细信息，请参阅[概念](https://msdn.microsoft.com/library/563e7e7c-65e1-44f4-b0b2-da04a6c1bc9e)。 某些特性由编译器直接解释。 其他特性则向程序源中插入代码，然后由编译器进行编译。 此类插入的代码通过减少你必须编写的代码量使编程变得更容易。 但有时 bug 可能导致应用程序在执行插入的代码时失败。 发生这种情况时，您可能希望查看插入的代码。 Visual Studio 提供两种查看插入的代码的方法：  
  
- 可以在“反汇编”窗口中查看插入的代码。  
  
- 使用 [/Fx](https://msdn.microsoft.com/library/14f0e301-3bab-45a3-bbdf-e7ce66f20560) 可以创建合并的源文件，其中包含原始代码和插入的代码。  
  
  “反汇编”窗口显示与源代码和特性所插入代码对应的汇编语言指令。 此外，“反汇编”窗口还可以显示源代码批注。  
  
### <a name="to-turn-on-source-annotation"></a>打开源批注  
  
- 右键单击“反汇编”窗口，然后从快捷菜单中选定“显示源代码”。  
  
     如果知道属性在源窗口中的位置，则可以使用快捷菜单在“反汇编”窗口中查找插入的代码。  
  
### <a name="to-view-injected-code"></a>查看插入的代码  
  
1. 调试器必须处于中断模式。  
  
2. 在源代码窗口中，将光标放在要查看其插入代码的特性前面。  
  
3. 右键单击并从快捷菜单中选择“转到反汇编”。  
  
     如果属性位置在当前执行点附近，则可以从“调试”菜单选择“反汇编”窗口。  
  
### <a name="to-view-the-disassembly-code-at-the-current-execution-point"></a>查看当前执行点处的反汇编代码  
  
1. 调试器必须处于中断模式。  
  
2. 从“调试”菜单中选择“窗口”，然后单击“反汇编”。  
  
## <a name="see-also"></a>请参阅  
 [调试器安全](../debugger/debugger-security.md)   
 [调试本机代码](../debugger/debugging-native-code.md)
