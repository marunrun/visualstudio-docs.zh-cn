---
title: 如何：使用反汇编窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.disassembly
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
- assembly language, debugging inline assembly code
- breakpoints, Disassembly window
- Disassembly window
- machine code
ms.assetid: eaf84dd0-c82d-481b-af51-690b74e7794c
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c25c3cdeb96abacb4123b2d0a851ac3d4acb0cd5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696142"
---
# <a name="how-to-use-the-disassembly-window"></a>如何：使用反汇编窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此功能是启用了地址级调试后才可用**选项**对话框中，**调试**节点。 但对于脚本或 SQL 调试是不可用的。  
  
 “反汇编”窗口显示与编译器所创建的指令对应的汇编代码。 如果正在调试托管代码，则这些汇编指令对应于由实时 (JIT) 编译器创建的本机代码，而不是由 Visual Studio 编译器生成的 Microsoft 中间语言 (MSIL)。  
  
 除汇编指令外，“反汇编”窗口还可显示下列可选信息：  
  
- 每条指令所在的内存地址 对于本机应用程序，这是实际内存地址。 对于 Visual Basic、C# 或托管代码，这是距离函数开头的偏移量。  
  
- 程序集代码派生于的源代码。  
  
- 代码字节 — 实际计算机或 MSIL 指令的字节表示形式。  
  
- 内存地址的符号名。  
  
- 对应于源代码的行号。  
  
  汇编语言指令由助记符（指令名称的缩写）和代表变量、寄存器以及常量的符号所组成。 每一条机器语言指令由一个汇编语言助记符代表，通常其后还跟有一个或多个变量、寄存器或常量。  
  
  如果您无法阅读汇编语言但又想充分利用“反汇编”窗口，请参考有关汇编语言编程的好书。 汇编语言编程超出了我们对“反汇编”窗口进行简单介绍的讨论范围。  
  
  汇编语言代码在很大程度上依赖处理器的寄存器（对托管代码而言，依赖公共语言运行时寄存器），您将发现协同使用“反汇编”窗口和“寄存器”窗口将很有用，可以允许您检查寄存器内容。  
  
  你很可能愿意使用汇编语言，而从来不会愿意或需要查看原始的、数字形式的机器代码指令。 不过，如果愿意的话，可以利用“内存”窗口或从“反汇编”窗口的快捷菜单中选取“代码字节”来查看。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-display-the-disassembly-window"></a>显示“反汇编”窗口  
  
- 上**调试**菜单中，选择**Windows**，然后单击**反汇编**。  
  
     调试器必须正在运行或处于中断模式。  
  
### <a name="to-turn-optional-information-on-or-off"></a>打开或关闭可选信息  
  
- 右键单击**反汇编**窗口中，并设置或清除快捷菜单中的所需的选项。  
  
     左边距中的黄色箭头表示当前执行点的位置。 对于本机代码，这对应于 CPU 的程序计数器。 该位置显示程序中将要执行的下一条指令。  
  
     有关详细信息，请参阅[向上分页或在内存中的向下](../debugger/how-to-page-up-or-down-in-memory.md)。  
  
## <a name="see-also"></a>请参阅  
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)   
 [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)
