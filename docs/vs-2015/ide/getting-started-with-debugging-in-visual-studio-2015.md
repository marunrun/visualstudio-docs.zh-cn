---
title: 在 Visual Studio 2015 中调试入门 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: c3a14d28-d811-4ff3-bd09-21dce14025ca
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: dfa68202d7f73d45b8422bb34c90954528d6af7b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68177832"
---
# <a name="getting-started-with-debugging-in-visual-studio-2015"></a>在 Visual Studio 2015 中调试入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 2015 提供一组强大的集成项目生成和调试工具。 本主题将介绍如何开始使用一组最基本的调试 UI 功能。

 注意：此页底部有指向更高级功能以及特定于平台或功能的主题的链接。

## <a name="my-code-doesnt-work-help-me-visual-studio-2015"></a>我的代码不起作用。 Visual Studio 2015，求助！
 你已经想到了编辑器并创建了一些代码。 现在，你想要开始调试该代码。 与大多数 IDE 一样，Visual Studio 2015 有两个调试阶段：生成代码以捕获并解决项目和编译器错误；在环境中运行代码以捕获并解决运行时和动态错误。

### <a name="configuring-a-build"></a>配置生成
 生成配置有两种基本类型：**调试**和**发布**。 第一种配置生成更慢、更大的可执行文件，此可执行程序实现更丰富的交互式运行时调试体验，但应永远不会投入市场销售。 第二种配置生成更快、更优化的可执行文件，此可执行文件适合投入市场销售（至少从编译器的角度来看是这样）。

 默认的生成配置是**调试**。

 ![Visual Studio 调试生成按钮](../ide/media/vs-ide-gs-debug-build-type1.PNG "Vs_ide_gs_debug_build_type1")

 你还可以指定要面向的特定的生成平台，如 **x86**（32 位 Intel CPU）、**x64**（64 位 Intel CPU）和 **ARM**（ARM CPU，仅支持某些应用类型）。 对于托管项目和本机项目，默认值为 **x86** 平台。 若要更改此值，请单击生成平台下拉列表，并选择其他平台或“配置管理器...” 

 ![Visual Studio“配置文件管理器”窗口](../ide/media/vs-ide-gs-debug-build-cf-mgr.PNG "Vs_ide_gs_debug_build_cf_mgr")

 可以使用“配置管理器”  指定要面向的生成配置。 启动管理器，单击“配置”  或“CPU”  下拉列表，然后选择“新建...”  创建新的生成或平台。

 ![Visual Studio“配置管理器”窗口](../ide/media/vs-ide-gs-debug-build-cf-mgr-2.PNG "Vs_ide_gs_debug_build_cf_mgr_2")

 刚开始时，只使用**调试**和 **x86** 分别作为生成配置和平台。 完成编码和调试时，将配置更改为**发布**并指定特定的平台。 （较旧版本的 Visual Studio 为 .Net 代码项目提供了 **AnyCPU** 默认平台。）

 注意：生成项目时，配置和平台值还用于确定创建哪些项目目录路径用于存储可执行文件。 通常，此路径为 **\<path-to-project>\\<project-name>\><configuration\\\><platform\\\>** 。 例如，配置为 `Debug`、平台为 `x86` 的项目位于 `Projects\MyProjectNameHere\MyProjectNameHere\bin\Debug\x86` 下面。 这在你拥有自己的工具和脚本来管理这些生成可执行文件时非常有用。

### <a name="building-your-code"></a>生成你的代码
 配置好生成后，即可实际生成项目。 最简单的方法是按 F7，但是还可以在主菜单中选择“生成”->“生成解决方案”来开始生成项目。 

 ![Visual Studio 生成项目菜单选择](../ide/media/vs-ide-gs-debug-build-menu-item.png "Vs_ide_gs_debug_build_menu_item")

 可以在 Visual Studio UI 底部的“输出”状态窗口中观察生成过程。  该窗口将显示错误、警告和生成操作。 如果出现错误（或者在配置的级别出现警告），你的生成将失败。 你可以单击错误和警告以转到出现错误和警告的行。 通过再次按 **F7**（仅重新编译出现错误的文件）或按 **Ctrl+Alt+F7**（适用于全新且完整的重新生成）重新生成项目。

 编辑器下方的结果窗口中有两个生成选项卡式窗口：**输出**窗口（它包含原始编译器输出，包括错误消息）和**错误列表**窗口（它提供所有错误和警告的可排序和可筛选列表）。

 如果操作成功，可在**输出**窗口中看到类似以下结果。

 ![Visual Studio 成功的生成输出](../ide/media/vs-ide-gs-debug-success-build.PNG "vs_ide_gs_debug_success_build")

### <a name="reviewing-the-error-list"></a>审阅错误列表
 除非你已对之前成功编译的代码进行了修改，否则很可能出现错误。 如果你不熟悉编码，则很可能出现许多错误。 错误有时很明显，如简单的语法错误或不正确的变量名，有时它们则难以理解，只有一个神秘代码显示给你。 有关这些问题更清晰的视图，请导航至生成“输出”窗口的底部，然后单击“错误列表”选项卡。   在此选项卡中，你可以看到关于项目错误和警告的一个更有条理的视图，并为你提供一些额外的选项。

 ![Visual Studio 2015 输出和错误列表](../ide/media/vs-ide-gs-debug-bad-build-error-list.PNG "Vs_ide_gs_debug_bad_build_error_list")

 单击“错误列表”窗口中的错误行，并跳转至发生错误的行。  （或单击右上侧的“快速启动”  栏，在其中键入行号，然后按 Enter，以打开行号。 这是转至“选项”  窗口条目最快的方法，你可以在这里打开行号。 了解如何使用“快速启动”  栏，可以省去多次单击 UI！）

 ![具有行号的 Visual Studio 编辑器](../ide/media/vs-ide-gs-debug-line-numbers.png "Vs_ide_gs_debug_line_numbers")

 ![Visual Studio 行号选项](../ide/media/vs-ide-gs-debug-options-line-numbers.png "Vs_ide_gs_debug_options_line_numbers")

 使用 Ctrl+G 快速跳转至发生错误的行号。

 错误由红色的“波形曲线”下划线标识。 将鼠标悬停在下划线上以获取其他详细信息。 修复后下划线消失，尽管纠正过程中可能会引入新的错误。 （此过程被称为“回归测试”。）

 ![Visual Studio 错误悬停](../ide/media/vs-ide-gs-debug-error-hover1.png "Vs_ide_gs_debug_error_hover1")

 遍历错误列表，并解决代码中的所有错误。

 ![Visual Studio 调试错误窗口](../ide/media/vs-ide-gs-debug-error-list.PNG "Vs_ide_gs_debug_error_list")

### <a name="reviewing-errors-in-detail"></a>审阅错误的详细信息
 许多错误可能对你没有意义，这些错误被当做编译器中的术语。 在这些情况下，你将需要其他信息。 在“错误列表”窗口中，可以通过右键单击相应条目行并从上下文菜单中选择“显示错误帮助”，执行自动必应搜索以获取错误（或警告）的详细信息。  

 ![Visual Studio 错误列表的必应搜索](../ide/media/vs-ide-gs-debug-error-list-error-help.png "Vs_ide_gs_debug_error_list_error_help")

 这将启动 Visual Studio 2015 内的一个选项卡，该选项卡承载错误代码和文本的 Bing 搜索结果。 结果来自 Internet 上许多不同的源，并且不是全部有用。

 你也可以单击“错误列表”的“代码”列中的超链接错误代码值。   这将启动该错误代码的 Bing 搜索。

### <a name="performing-static-code-analysis"></a>执行静态代码分析
 “静态代码分析”是“自动检查我的代码是否存在可能导致运行时错误或代码管理问题的常见问题”的流行说法。 养成在清除了阻止生成的明显错误后运行该分析的习惯，然后花一些时间解决其可能产生的警告。 你将为自己省去一些将来的麻烦，并了解几种代码样式技术。

 按 Alt+F11（或从顶部菜单选择“分析”->“对解决方案运行代码分析”  ）以启动静态代码分析。 如果你有大量代码，这可能需要一些时间。

 ![Visual Studio 2015 代码分析菜单项](../ide/media/vs-ide-gs-debug-run-code-analysis.png "Vs_ide_gs_debug_run_code_analysis")

 任何新的或更新的警告都将显示在 IDE 底部的“错误列表”选项卡中。  单击警告以跳转到相应的行。

 ![Visual Studio 2015 错误列表但出现警告](../ide/media/vs-ide-gs-debug-code-analysis-warning-error-list.PNG "vs_ide_gs_debug_code_analysis_warning_error_list")

 警告将用明亮的黄绿色（而非红色）波形曲线标识。 将鼠标悬停在波形曲线上方以获取详细信息，右键单击波形曲线获取获取上下文菜单以帮助修复或重构选项。

 ![Visual Studio 代码分析警告悬停](../ide/media/vs-ide-gs-debug-code-analysis-warning-hover.png "vs_ide_gs_debug_code_analysis_warning_hover")

### <a name="using-light-bulbs-to-fix-or-refactor-code"></a>使用灯泡修复或重构代码
 电灯泡是 Visual Studio 2015 的新增功能，使用此功能可重构代码内联。 灯泡是快速、高效修复常见问题的简单方法。 若要使用灯泡，请右键单击某个警告波形曲线（或在将鼠标悬停在波形曲线上时按 Ctrl+. ），然后选择“快速操作”  。

 ![Visual Studio 2015 灯泡快速选项](../ide/media/vs-ide-gs-debug-light-bulb1.png "Vs_ide_gs_debug_light_bulb1")

 你将看到可应用于代码行的可能修复或重构方法列表。

 ![Visual Studio 2015 灯泡预览](../ide/media/vs-ide-gs-debug-light-bulb-preview-changes.PNG "Vs_ide_gs_debug_light_bulb_preview_changes")

 只要代码分析器确定有机会修复、重构或改进你的代码，就能使用灯泡。 单击任意代码行，右键单击以打开上下文菜单，然后选择“快速选项”  （或者如果希望效率优先，请再次按 Ctrl+）。 如果有可用的区域重构或改进选项，将显示这些选项；否则，IDE 的左下角面板将显示消息 `No quick options available here`。

 ![Visual Studio 2015 灯泡无选项文本](../ide/media/vs-ide-gs-debug-light-bulb-no-options.PNG "Vs_ide_gs_debug_light_bulb_no_options")

 根据经验，你可以快速使用箭头键和 Ctrl+。 检查“快速选项”重构机会并清理你的代码！

 有关灯泡的详细信息，请阅读[使用灯泡执行快速操作](../ide/perform-quick-actions-with-light-bulbs.md)。

### <a name="debugging-your-running-code"></a>调试运行代码
 现在你已成功生成了代码并执行了一些清理，请按 F5 或者选择“调试”->“开始调试”来运行代码。  这将在调试环境中启动你的应用，便于你观察其详细行为。 Visual Studio 2015 IDE 在应用运行时更改：“输出”窗口由两个新窗口代替（在默认的窗口配置中），这两个新窗口分别是“自动/局部变量/模块/监视”选项卡式窗口和“调用堆栈/断点/异常设置/输出”选项卡式窗口    。 这两个窗口具有多个选项卡，可用于检查和评估应用的变量、线程、调用堆栈及其运行时的各种其他行为。

 ![VS2015 自动和调用堆栈 Windows](../ide/media/vs-ide-gs-debug-autos-and-call-stack.PNG "Vs_ide_gs_debug_autos_and_call_stack")

 用你的应用尝试各种操作，然后观察更改。 如果出现异常，请按 Ctrl + Alt + Break 暂停应用程序（或单击“暂停”  按钮）。

 ![Visual Studio“全部中断”按钮](../ide/media/vs-ide-gs-debug-break-all-button.png "vs_ide_gs_debug_break_all_button")

 按 F5 继续运行应用程序（或单击“继续”  按钮）。

 ![Visual Studio“继续调试”按钮](../ide/media/vs-ide-gs-debug-continue-button.png "Vs_ide_gs_debug_continue_button")

 按 Shift + F5 或单击“停止”  按钮可以停止应用程序。 或者，你可以仅关闭应用的主窗口（或命令行对话框）。

 如果你的代码按预期完美而准确地运行，祝贺你！ 将生成配置更改为**发布**并重新生成以进行部署！ （尽管专业人员可能想要在结束时跳转到单元测试上的位。）但是，如果它挂起、崩溃，或为您带来一些奇怪的结果，你需要找到这些问题的根源并修复 bug。

### <a name="setting-simple-breakpoints"></a>设置简单断点
 断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。 在设置或移除断点后，你不需要重新生成项目。

 通过单击想要发生中断的行的远端边距来设置一个断点，或选择代码行并按 F9。 运行代码时，它将在执行此代码行的说明之前停止。

 ![Visual Studio 断点](../ide/media/vs-ide-gs-debug-breakpoint1.png "Vs_ide_gs_debug_breakpoint1")

 代码中断时，标记的代码行尚未执行。 此时，你可能想要执行由断点标记的代码行的说明，并检查更改的值。 这称为“单步执行”代码。 如果标记的代码是方法调用，可以按 F11 单步执行它。 你还可以按 F10“逐过程”执行该代码行。 有关断点步骤操作的详细信息，请阅读[使用调试器在代码中导航](../debugger/navigating-through-code-with-the-debugger.md)。

 断点的常见用途包括：

1. 缩小崩溃或挂起的根源，将它们分散在你认为引起失败的方法调用的代码中。 单步执行代码时，请移除断点，然后重设断点使其更紧密，直到找到有问题的代码行。

2. 引入新代码时，请在代码的开头设置断点并单步执行代码，以确保它按预期方式运行。

3. 如果已实现复杂的行为，请为算法代码设置断点，以便在程序中断时检查变量和数据的值。

4. 如果正在编写 C 或 C++ 代码，请使用断点停止该代码，以便在调试内存相关故障时检查地址值（查找 NULL）和引用计数。

   有关使用断点的详细信息，请参阅[使用断点](../debugger/using-breakpoints.md)。

### <a name="setting-conditional-breakpoints"></a>设置条件断点
 如果循环或递归中存在断点，或者有许多频繁单步执行的断点，请使用条件断点以确保你的代码仅在满足特定条件时挂起。 否则，你将会按很多次 F11。

 若要在变量设置为某个特定值或传递某个特定阈值时设置条件断点并挂起你的代码，请在边距中单击以设置断点，然后从出现的悬停菜单中选择“嵌齿”。

 ![Visual Studio 2015 断点设置](../ide/media/vs-ide-gs-debug-breakpoint-settings.png "Vs_ide_gs_debug_breakpoint_settings")

 你将看到如下对话框，可以在此对话框中为中断的发生设置特定条件。

 ![Visual Studio 2015 条件断点](../ide/media/vs-ide-gs-debug-breakpoint-conditional.PNG "Vs_ide_gs_debug_breakpoint_conditional")

 有关如何声明用于评估条件断点的表达式的详细信息，请观看第 9 频道视频 [Visual Studio 2015 中的断点配置体验](http://channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/711)。

### <a name="inspecting-your-code-at-run-time"></a>在运行时检查你的代码
 当运行代码达到断点并暂停时，你可以检查变量和调用堆栈以确定发生了什么情况。 这些值是否在你期望的范围内？ 调用是否正按正确的顺序进行？

 ![运行 visual Studio 2015&#45;值检查的时间](../ide/media/vs-ide-gs-debug-inspect-value.PNG "vs_ide_gs_debug_inspect_value")

 将鼠标悬停在变量上以查看它当前包含的值和引用。 如果你看到一个意外的值，表示代码的前一行或调用行可能出现了 bug。 将断点上移或向现有断点添加条件，以进一步缩小搜索范围。

 此外，Visual Studio 2015 会显示诊断工具窗口，随着时间的推移，你可以在此窗口中观察应用的 CPU 和内存使用率。 使用它们来查找意外的高 CPU 使用率或内存分配。 结合使用“监视”窗口和断点，以确定什么原因导致意外的高使用率或未释放的资源。 

 ![Visual Studio 2015 诊断工具窗口](../ide/media/vs-ide-gs-debug-diagnostic-tools.PNG "Vs_ide_gs_debug_diagnostic_tools")

### <a name="running-unit-tests"></a>运行单元测试
 单元测试是在你的应用或服务中练习代码路径的程序。 Visual Studio 2015 安装了适用于托管和本机代码的 Microsoft 单元测试框架。 使用单元测试框架创建单元测试，运行测试，然后报告这些测试的结果。 进行更改后重新运行单元测试，以测试代码仍能正常工作。 使用 Visual Studio 2015 Enterprise 时，你可以在每次生成后自动运行测试。

 请阅读[使用 IntelliTest 为代码生成单元测试](../test/generate-unit-tests-for-your-code-with-intellitest.md)获取入门指南。

 若要了解有关 Visual Studio 2015 中的单元测试以及它们如何帮助你创建更高质量代码的详细信息，请阅读[单元测试基础知识](../test/unit-test-basics.md)。

## <a name="see-also"></a>另请参阅
 [在 Visual Studio 中调试](../debugger/debugging-in-visual-studio.md)[调试器设置和准备](../debugger/debugger-settings-and-preparation.md)[调试 64 位应用程序](../debugger/debug-64-bit-applications.md)[调试器基础知识](../debugger/debugger-basics.md)
