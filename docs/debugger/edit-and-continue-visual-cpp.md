---
title: 编辑并继续（C++） |Microsoft Docs
ms.date: 05/31/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C++]
- debugging [C++], Edit and Continue
- C/C++, Edit and Continue
ms.assetid: 1815251e-a877-433e-9e5e-69bd9ba254c7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 0ebe31267ee666250fbaeda73f1678051f1d4727
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72435853"
---
# <a name="edit-and-continue-c"></a>编辑并继续（C++）
可以在项目中使用 "编辑C++并继续"。 请参阅[支持的代码更改 (C++)](../debugger/supported-code-changes-cpp.md)，了解有关 Edit and Continue 的限制的信息。

有关 Visual Studio 2015 Update 3 功能改进的详细信息，请参阅 [Visual Studio 2015 Update 3 中的 C++ Edit and Continue](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)。

 Visual Studio 2013 Update 3 中引入的编译器选项 [/Zo（增强优化调试）](/cpp/build/reference/zo-enhance-optimized-debugging) 向 .pdb （符号） 文件中添加了其他信息，用于未使用 [/Od（禁用（调试））](https://msdn.microsoft.com/library/aafb762y.aspx)选项编译的二进制文件。

 **/Zo** 禁用 Edit and Continue。 请参阅[如何：调试优化的代码](../debugger/how-to-debug-optimized-code.md)。

## <a name="BKMK_Enable_or_disable_automatic_invocation_of_Edit_and_Continue"></a> 启用或禁用“编辑并继续”
 如果要对代码进行编辑而又不希望在当前调试会话过程中应用这些编辑，则可以禁用自动调用“编辑并继续”。 也可以重新启用“编辑并继续”的自动操作。

> [!IMPORTANT]
> 有关所需生成设置和功能兼容性的其他信息，请参阅 [Visual Studio 2015 Update 3 中的 C++“编辑并继续”](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)。

1. 如果在调试会话中，请停止调试（**Shift + F5**）。

2. 在 **“工具”** 菜单上，选择 **“选项”** 。

3. 在“选项”对话框中，选择“调试”>“常规”。

4. 若要启用，请选择 "**启用编辑并继续**"。 若要禁用，请清除该复选框。

5. 在“Edit and Continue”组中，选中或取消选中“启用本机 Edit and Continue”复选框。

   更改此设置将影响当前处理的所有项目。 更改此设置后不需要重新生成应用程序。 如果从命令行或生成文件生成应用程序，但在 Visual Studio 环境中调试，则仍可以使用 Edit and Continue（如果已设置“/ZI”选项）。

## <a name="BKMK_How_to_apply_code_changes_explicitly"></a> 如何显式应用代码更改
 在C++中，"编辑并继续" 可通过两种方式应用代码更改。 代码更改可在选择执行命令时隐式应用，也可使用 **“应用代码更改”** 命令显式应用。

 选择执行命令时可以隐式应用代码更改；

- 或者，使用“应用代码更改”命令则可以显式应用代码更改。

## <a name="BKMK_How_to_stop_code_changes"></a> 如何停止代码更改
 当“编辑并继续”处于应用代码更改的过程中时，您可以停止该操作。

 要停止应用代码更改：

- 在 **调试** 菜单中选择 **停止应用代码更改**。

  该菜单项仅在应用代码更改时才可见。

  如果选择了改选项，就不会进行任何代码更改。

## <a name="BKMK_How_to_reset_the_point_of_execution"></a> 如何重置执行点
 在“编辑并继续”应用更改时，一些代码更改会使执行点移动到新的位置。 “编辑并继续”尽可能正确地放置执行点，但是并非所有情况下的结果都正确。

 在C++中，当执行点发生更改时，将向你发出通知。 在继续调试之前，应验证位置是否正确。 如果位置不正确，则使用**设置下一语句**命令。 有关详细信息，请参阅[设置下一个要执行的语句](https://msdn.microsoft.com/library/y740d9d3.aspx#BKMK_Set_the_next_statement_to_execute)。

## <a name="BKMK_How_to_work_with_stale_code"></a> 如何使用陈旧代码
 在某些情况下，“编辑并继续”无法将代码更改立即应用于可执行文件，但如果您继续调试，则可能会在稍后应用代码更改。 当编辑某个调用当前函数的函数，或将多于 64 个字节的新变量添加到调用堆栈上的函数时，就会发生这种情况。

 在这种情况下，调试器会继续执行原始代码，直至可以应用更改。 陈旧的代码在单独的源窗口中作为临时源文件窗口显示，并带有一个类似 `enc25.tmp`的标题。 编辑过的源继续在原始源窗口中显示。 当您尝试编辑陈旧的代码时，会显示一条警告信息。

## <a name="see-also"></a>请参阅
- [受支持的代码更改 (C++)](../debugger/supported-code-changes-cpp.md)