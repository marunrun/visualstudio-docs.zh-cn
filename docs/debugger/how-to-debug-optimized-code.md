---
title: 如何：调试优化的代码 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- breakpoints, in optimized code
- debugging [C++], optimized code
- optimization, debug builds
- debug builds, optimizing
- optimized code, debugging
ms.assetid: fc8eeeb8-6629-4c9b-99f7-2016aee81dff
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 590925a894f1bf9bfe70d9dd1bf6142fcb6a2e34
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430663"
---
# <a name="how-to-debug-optimized-code"></a>如何：调试优化的代码

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

> [!NOTE]
> [/Zo（增强优化调试）](/cpp/build/reference/zo-enhance-optimized-debugging)编译器选项（在 Visual Studio Update 3 中引入）为优化代码生成更丰富的调试信息（未使用“/Od”编译器选项生成的项目。 请参阅 [/O 选项（优化代码）](/cpp/build/reference/o-options-optimize-code)）。 这包括对调试本地变量和内联函数的改进的支持。
>
> “/Zo”编译器选项时，禁用[编辑并继续](../debugger/edit-and-continue-visual-csharp.md)。

 当编译器优化代码时，它将重新定位并重组指令， 这会得到更高效的编译的代码。 由于这种调整，调试器并不总能确定与一组指令对应的源代码。

 优化可能影响到：

- 本地变量（可被优化器移除或移动到调试器无法识别的位置）。

- 函数内部的位置（当优化器合并代码块时发生变化的位置）。

- 调用堆栈上框架的函数名称（如果优化器合并两个函数，则函数名称可能是错误的）。

  但是，假定所有框架都有符号，则在调用堆栈上看到的框架几乎总是正确的。 在下列情况下调用堆栈上的框架将是错误的：有堆栈损坏，有用汇编语言编写的函数，或者有操作系统框架在调用堆栈上没有匹配的符号。

  全局和静态变量总是正确显示。 结构布局也是这样。 如果您有指向结构的指针而且指针的值是正确的，那么结构的每个成员变量都将显示正确值。

  出于这些限制原因，只要有可能，就应使用程序的“未优化”版本进行调试。 默认情况下，优化在 C++ 程序的“调试”配置中处于关闭状态，在“发布”配置中处于打开状态。

  但是，bug 可能仅在程序的优化版本中出现。 在此情况下，必须调试优化的代码。

## <a name="to-turn-on-optimization-in-a-debug-build-configuration"></a>在“Debug”生成配置中打开优化

1. 创建新项目时，请选择 `Win32 Debug`目标。 接下来要一直使用 `Win32``Debug` 目标，直至程序已进行全面调试并可以生成 `Win32 Release` 目标为止。 调试器并不优化 `Win32 Debug`目标。

2. 在解决方案资源管理器中选择项目。

3. 在“视图”菜单上，单击“属性页” 。

4. 在“属性页”对话框中，确保在“配置”下拉列表框中选择了 `Debug` 。

5. 在左边的文件夹视图中，选择“C/C++”文件夹。

6. 在“C++”文件夹下，选择 `Optimization`。

7. 在右边的属性列表中找到“`Optimization`”。 它旁边的设置可能显示为 `Disabled (`[/Od](/cpp/build/reference/od-disable-debug)`)`。 选择其他选项（`Minimum Size``(`[/O1](/cpp/build/reference/o1-o2-minimize-size-maximize-speed)`)`、`Maximum Speed``(`[/O2](/cpp/build/reference/o1-o2-minimize-size-maximize-speed)`)`、`Full Optimization``(`[/Ox](/cpp/build/reference/ox-full-optimization)`)` 或 `Custom`）之一。

8. 如果为“`Custom`”选择了“`Optimization`”选项，现在便可为属性列表中显示的其他任何属性设置选项。

9. 选择项目属性页中的配置属性、C/C++、命令行节点，并将 `(`[/Zo](/cpp/build/reference/zo-enhance-optimized-debugging)`)` 添加到“其他选项”文本框。

    > [!WARNING]
    > `/Zo` 需要 Visual Studio 2013 Update 3 或更高版本。
    >
    >  添加 `/Zo` 将禁用[编辑并继续](../debugger/edit-and-continue-visual-csharp.md)。

   调试优化的代码时，请使用“反汇编”窗口以了解实际创建和执行的指令。 设置断点时，需要注意断点可能随指令一起移动。 例如，考虑以下代码：

```cpp
for (x=0; x<10; x++)
```

 假定在该行设置了一个断点。 可能希望该断点被命中 10 次，但如果代码进行了优化，则只会命中该断点一次。 因为第一个指令将 `x` 的值设置为 0。 编译器认定该指令只需执行一次，将其移出循环。 断点随之移动。 而比较和递增 `x` 的指令仍留在循环内。 查看“反汇编”窗口时，[单步执行单元](/previous-versions/visualstudio/visual-studio-2010/ek13f001(v=vs.100))自动设置为“指令”以允许更大控制，这在逐句通过优化的代码时很有用。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [调试本机代码](../debugger/debugging-native-code.md)