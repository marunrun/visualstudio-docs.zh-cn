---
title: 在调试器中查看反汇编代码 | Microsoft Docs
ms.custom: seodec18
ms.date: 10/30/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.disassembly
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- assembly language, debugging inline assembly code
- breakpoints, Disassembly window
- Disassembly window
- machine code
ms.assetid: eaf84dd0-c82d-481b-af51-690b74e7794c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43214ee122b3aa5c3907b9176631f2dc22c9178e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62846385"
---
# <a name="view-disassembly-code-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>在 Visual Studio 调试器中查看反汇编代码（C#、C++、Visual Basic、F#）

“反汇编”窗口显示与编译器所创建的指令对应的汇编代码。 如果正在调试托管代码，则这些汇编指令对应于由实时 (JIT) 编译器创建的本机代码，而不是由 Visual Studio 编译器创建的 Microsoft 中间语言 (MSIL)。

> [!NOTE]
> 若要充分利用“反汇编”窗口，请了解或学习[汇编语言编程](https://wikipedia.org/wiki/Assembly_language)的基础知识。

只有启用了地址级调试后，此功能才可用。 它不适用于脚本或 SQL 调试。

除汇编指令外，“反汇编”窗口还可显示下列可选信息：

- 每条指令所在的内存地址 对于本机应用程序，它是实际内存地址。 对于 Visual Basic 或 C#，它是距离函数开头的偏移量。

- 程序集代码派生于的源代码。

- 代码字节，即实际计算机或 MSIL 指令的字节表示形式。

- 内存地址的符号名。

- 对应于源代码的行号。

汇编语言指令由助记符（指令名称的缩写）和代表变量、寄存器以及常量的符号组成。 每一条机器语言指令由一个汇编语言助记符表示，（可选）后跟一个或多个符号。

汇编代码在很大程度上依赖于处理器寄存器；对于托管代码，则依赖于公共语言运行时寄存器。 可以将“反汇编”窗口与“寄存器”窗口一起使用，以便检查寄存器内容。

若要以原始数字形式而不是汇编语言查看机器代码指令，请使用“内存”窗口，或从“反汇编”窗口的快捷菜单中选择“代码字节”。

## <a name="use-the-disassembly-window"></a>使用“反汇编”窗口

若要启用“反汇编”窗口，请在“工具” > “选项”（或“工具” > “选项”）>“调试”下，选择“启用地址级调试”。

若要在调试期间打开“反汇编”窗口，请选择“窗口” > “反汇编”或按 Alt+8 。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

若要打开或关闭可选信息，请在“反汇编”窗口中单击右键，然后在快捷菜单中设置或清除所需的选项。

左边距中的黄色箭头表示当前执行点。 对于本机代码，该执行点对应于 CPU 的程序计数器。 该位置显示程序中将要执行的下一条指令。

## <a name="see-also"></a>请参阅

* [在内存中向上或向下翻页](../debugger/how-to-page-up-or-down-in-memory.md)
* [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
* [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)