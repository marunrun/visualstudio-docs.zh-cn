---
title: 修复程序错误并改进代码
description: 本文介绍 Visual Studio 可帮助查找和修复代码中的问题（包括生成错误、代码分析、调试工具和单元测试）的一些基本方法。
ms.date: 05/02/2018
ms.topic: conceptual
ms.assetid: c3a14d28-d811-4ff3-bd09-21dce14025ca
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e66d0d1ed8115b214b1da1654cbefdc96f7d1774
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588611"
---
# <a name="make-code-work-in-visual-studio"></a>确保代码在 Visual Studio 中正常运行

Visual Studio 提供了一组功能强大的项目构建和调试工具。 在本文中，您将了解 Visual Studio 如何使用生成输出、代码分析、调试工具和单元测试来帮助您在代码中查找问题。

你已经想到了编辑器并创建了一些代码。 现在，需要确保代码正确运行。 与大多数 IDE 一样，Visual Studio 通过两个阶段确保代码正常运行：生成代码以捕获并解决项目和编译器错误，以及运行代码以查找运行时和动态错误。

## <a name="build-your-code"></a>生成代码

生成配置有两种基本类型：“调试”和“发布”   。 Debug 配置生成较慢、较大的可执行文件，它们允许更丰富的交互式运行时调试体验  。 不应发布 Debug 可执行文件  。 Release 配置生成较快、经过优化的可执行文件，它们适合用于发布（至少从编译器的角度看）  。 默认的生成配置是**调试**。

生成项目最简单的方法是按 F7，但是还可以在主菜单中选择“生成” > “生成解决方案”开始生成项目    。

![Visual Studio 生成项目菜单选择](../ide/media/vs_ide_gs_debug_build_menu_item.png)

可以在 Visual Studio UI 底部的“输出”窗口中观察生成过程  。 该窗口将显示错误、警告和生成操作。 如果出现错误（或者在配置的级别出现警告），则生成失败。 你可以单击错误和警告以转到出现错误和警告的行。 通过再次按 F7（仅重新编译出现错误的文件）或按 Ctrl+Alt+F7（适用于全新且完整的重新生成）重新生成项目     。

编辑器下方的结果窗口中有两个选项卡式窗口：“输出”窗口（它包含原始编译器输出，包括错误消息）和“错误列表”窗口（它提供所有错误和警告的可排序和可筛选列表）   。

如果生成成功，可在“输出”窗口中看到类似以下结果  ：

![Visual Studio 成功生成输出](../ide/media/vs_ide_gs_debug_success_build.png)

## <a name="review-the-error-list"></a>审阅错误列表

除非未对之前成功编译的代码进行修改，否则很可能出现错误。 如果不熟悉编码，则可能出现许多错误。 错误有时很明显，如简单的语法错误或不正确的变量名，有时它们则难以理解，只有一个神秘代码显示给你。 有关这些问题更清晰的视图，请导航至生成“输出”窗口的底部，然后单击“错误列表”选项卡。   在此选项卡中，你可以看到关于项目错误和警告的一个更有条理的视图，并为你提供一些额外的选项。

![Visual Studio 输出和错误列表](../ide/media/vs_ide_gs_debug_bad_build_error_list.png)

单击“错误列表”窗口中的错误行，跳转至发生错误的行  。 （或按 Ctrl+Q   ，键入行号  ，然后从结果中选择“打开或关闭行号”  来打开行号。 这是转至“选项”  对话框最快的方法，可以在此打开行号。）

![Visual Studio 具有行号的编辑器](../ide/media/vs_ide_gs_debug_line_numbers.png)

![Visual Studio 行号选项](../ide/media/vs_ide_gs_debug_options_line_numbers.png)

按 Ctrl+G 快速跳转至发生错误的行号   。

错误由红色的“波形曲线”下划线标识。 将鼠标悬停在下划线上以获取其他详细信息。 修复后下划线消失，尽管纠正过程中可能会引入新的错误。 （此过程被称为“回归”。）

![Visual Studio 错误悬停](../ide/media/vs_ide_gs_debug_error_hover1.png)

遍历错误列表，并解决代码中的所有错误。

![Visual Studio“调试错误”窗口](../ide/media/vs_ide_gs_debug_error_list.png)

### <a name="review-errors-in-detail"></a>审阅错误的详细信息

许多错误可能对你没有意义，这些错误被当做编译器中的术语。 在这些情况下，将需要其他信息。 从“错误列表”窗口，可以自动进行必应搜索，以获取有关错误或警告的详细信息  。 右键单击相应的条目行并从上下文菜单选择“显示错误帮助”，或者单击“错误列表”的“代码”列中的超链接错误代码值    。

![Visual Studio 错误列表必应搜索](../ide/media/vs_ide_gs_debug_error_list_error_help.png)

根据设置，Web 浏览器显示错误代码和文本的搜索结果，或者在 Visual Studio 内打开选项卡并显示必应搜索的结果。 结果来自 Internet 上许多不同的源，并且不是全部有用。

## <a name="use-code-analysis"></a>使用代码分析

代码分析器查找可导致运行时错误或代码管理问题的常见代码问题。

### <a name="c-and-visual-basic-code-analysis"></a>C# 和 Visual Basic 代码分析

Visual Studio 包括一系列内置的 [.NET Compiler Platform 分析器](../code-quality/roslyn-analyzers-overview.md)，这些分析器在用户键入时检查 C# 和 Visual Basic 代码。 可以将其他分析器作为 Visual Studio 扩展或 NuGet 包安装。 如果发现规则冲突，将同时在错误列表和代码编辑器（违规代码下方有波浪线）中报告。

### <a name="c-code-analysis"></a>C++ 代码分析

若要分析 C++ 代码，请运行[静态代码分析](../code-quality/quick-start-code-analysis-for-c-cpp.md)。 养成在清除了阻止生成的明显错误后运行该分析的习惯，然后花一些时间解决其可能产生的警告。 这可避免将来的一些麻烦，并且你可由此了解一些代码样式技术。

按 Alt+F11（或从顶部菜单选择“分析” > “对解决方案运行代码分析”）启动静态代码分析     。

![Visual Studio 代码分析菜单项](../ide/media/vs_ide_gs_debug_run_code_analysis.png)

任何新的或更新的警告都将显示在 IDE 底部的“错误列表”选项卡中  。 单击警告以跳转到代码中相应的行。

![包含警告的 Visual Studio 错误列表](../ide/media/cpp-code-analysis-warning.png)

## <a name="use-quick-actions-to-fix-or-refactor-code"></a>使用“快速操作”修复或重构代码

通过灯泡或螺丝刀图标提供的 [快速操作](../ide/quick-actions.md)，可让您重构内联代码 它们是在 C#、C++ 和 Visual Basic 代码中快速、有效地修复常见警告的简便方法。 要访问它们，请右键单击警告波形并选择“快速操作和重构”  。 或者，在光标位于彩色波浪线所在行时，按 Ctrl+.   或选择边距中的灯泡、错误灯泡或螺丝刀图标。 您将看到可以应用于该行代码的可能修复或重构列表。

![Visual Studio 灯泡预览](../ide/media/quick-actions-options.png)

只要代码分析器确定有机会修复、重构或改进代码，就能使用“快速操作”。 单击任意代码行，右键单击以打开上下文菜单，然后选择“快速操作和重构”  。 如果重构或改进选项可用，则会显示。 否则，IDE 的左下角会显示消息“此处无可用的快速操作”  。

![“无可用的快速操作”文本](../ide/media/vs_ide_gs_debug_light_bulb_no_options.png)

根据经验，可以快速使用箭头键和 Ctrl+.   检查是否有简单的重构机会并清理代码！

::: moniker range="vs-2019"

## <a name="run-code-cleanup"></a>运行代码清理

通过编辑器底部的“代码清理”按钮，Visual Studio 提供[按需格式化 C# 代码文件](code-styles-and-code-cleanup.md#apply-code-styles)的功能，包括代码风格首选项  。

![Visual Studio 2019 中的“代码清理”按钮](media/execute-code-cleanup.png)

“代码清理”不仅可以设置文件的空格、缩进等格式，还可以应用一套定义的代码样式约定  。 将从 [EditorConfig 文件](code-styles-and-code-cleanup.md#code-styles-in-editorconfig-files)（若项目有此文件）或从“选项”对话框的[代码样式设置](code-styles-and-code-cleanup.md#code-styles-in-the-options-dialog-box)中读取对各个代码样式的偏好设置。 

::: moniker-end

## <a name="debug-your-running-code"></a>调试运行代码

现在已成功生成了代码并执行了一些清理，请按 F5 或者选择“调试” > “开始调试”来运行代码    。 这在调试环境中启动应用，便于观察其详细行为。 Visual Studio IDE 在应用运行时会发生变化：“输出”  窗口由两个新窗口代替（使用默认的窗口配置），这两个新窗口分别是“自动/局部变量/监视”  选项卡式窗口和“调用堆栈/断点/异常设置/输出”  选项卡式窗口。 这两个窗口具有多个选项卡，可用于检查和评估应用的变量、线程、调用堆栈及其运行时的各种其他行为。

![Visual Studio“自动”和“调用堆栈”窗口](../ide/media/vs_ide_gs_debug_autos_and_call_stack.png)

按 Shift+F5 或单击“停止”按钮停止应用    。 或者，可以仅关闭应用的主窗口（或命令行对话框）。

如果你的代码按预期完美而准确地运行，祝贺你！ 但是，如果它挂起、崩溃，或带来一些奇怪的结果，则需要找到这些问题的根源并修复 bug。

### <a name="set-simple-breakpoints"></a>设置简单断点

[断点](../debugger/using-breakpoints.md)是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。 在设置或删除断点后，不需要重新生成项目。

通过单击想要发生中断的行的远端边距来设置一个断点，或按 F9  在当前代码行上设置断点。 运行代码时，它将在执行此代码行的指令之前暂停（或中断  ）。

![Visual Studio 断点](../ide/media/vs_ide_gs_debug_breakpoint1.png)

断点的常见用途包括：

- 若要缩小故障或挂起的源范围，可将断点分散在你认为引起故障的方法调用的代码中。 在调试器中运行代码时，请移除断点，然后重设断点使其更紧密，直到找到有问题的代码行。 请参阅下一部分，了解如何在调试器中运行代码。

- 引入新代码时，请在代码的开头设置断点并运行代码，确保它按预期方式运行。

- 如果已实现复杂的行为，请为算法代码设置断点，以便在程序中断时检查变量和数据的值。

- 如果正在编写 C 或 C++ 代码，请使用断点停止该代码，以便在调试内存相关故障时检查地址值（查找 NULL）和引用计数。

有关使用断点的详细信息，请阅读[使用断点](../debugger/using-breakpoints.md)。

### <a name="inspect-your-code-at-run-time"></a>在运行时检查代码

运行的代码命中断点并暂停时，标记为黄色的代码行（当前语句）尚未执行。 此时，建议执行当前语句，然后检查更改的值。 可以使用多个 step  命令在调试器中执行代码。 如果标记的代码是方法调用，可以按 F11  单步执行它。 还可以按 F10  ，“逐过程”  执行该代码行。 有关其他命令及如何逐步执行代码的详细信息，请阅读[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。

![Visual Studio 运行时值检查](../ide/media/vs_ide_gs_debug_hit_breakpoint.png)

在上图中，可以按 F10  或 F11  使调试器前移一条语句（由于此处没有方法调用，因此这两个命令的结果相同）。

调试器暂停时，可以检查变量并调用堆栈来确定所出现的情况。 这些值是否在你期望的范围内？ 调用是否正按正确的顺序进行？

![Visual Studio 运行时值检查](../ide/media/vs_ide_gs_debug_inspect_value.png)

将鼠标悬停在变量上，查看其当前值和引用。 如果出现意外值，则表示前一代码或调用代码可能出现了 bug。 有关更深入的调试信息，请[了解更多](../debugger/debugger-feature-tour.md)使用调试器的信息。

此外，Visual Studio 显示“诊断工具”窗口，可从其中观察随时间变化的应用的 CPU 和内存使用情况  。 之后在开发应用时，可以使用这些工具查找意外的高 CPU 使用率或内存分配。 结合使用“监视”窗口和断点，确定导致意外的高使用率或未释放的资源的原因  。 有关详细信息，请参阅[分析功能简介](../profiling/profiling-feature-tour.md)。

## <a name="run-unit-tests"></a>运行单元测试

单元测试是防御代码 bug 的第一道防线，因为正确完成单元测试后，它们会测试一个“单元”的代码（一般是单个函数），并且调试起来比完整程序更简单。 Visual Studio 安装了适用于托管和本机代码的 Microsoft 单元测试框架。 使用单元测试框架创建单元测试，运行测试，然后报告这些测试的结果。 进行更改后重新运行单元测试，以测试代码仍能正常工作。 对于 Visual Studio 企业版，可以在每次生成后自动运行测试。

请阅读[使用 IntelliTest 为代码生成单元测试](../test/generate-unit-tests-for-your-code-with-intellitest.md)获取入门指南。

若要了解有关 Visual Studio 中的单元测试以及它们如何帮助创建更高质量代码的详细信息，请阅读[单元测试的基础知识](../test/unit-test-basics.md)。

## <a name="see-also"></a>请参阅

- [初探调试器](../debugger/debugger-feature-tour.md)
- [了解更多使用调试器的信息](../debugger/index.yml)
- [生成和修复代码](../ide/code-generation-in-visual-studio.md)
