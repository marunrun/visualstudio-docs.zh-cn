---
title: 运行应用商店应用的单元测试
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 5a6f5b32-bfce-4a63-81e9-02d54c592539
caps.latest.revision: 14
author: alexhomer1
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bfcdb3906f405b9f7ba4650be13f4522ab559ee8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446220"
---
# <a name="run-unit-tests-for-store-apps-in-visual-studio"></a>对 Visual Studio 中的应用商店应用运行单元测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题描述如何通过使用 Microsoft Visual Studio 中的测试资源管理器运行单元测试

> [!NOTE]
> 本部分中的主题描述了 Visual Studio Express for Windows 8 的功能。 Visual Studio Community、Enterprise. 和 Professional 提供其他适用于单元测试的功能。
>
> - 使用已为 Microsoft 测试资源管理器创建附加设备适配器的任何第三方或开放源代码单元测试框架。 还可为测试分析并显示代码覆盖率信息。
>   - 在每次生成后运行测试。 你也可以使用 Microsoft Fakes（托管代码的隔离框架），通过替换系统和第三方功能的测试代码将你的测试集中于你自己的代码之上。
>
>   有关详细信息，请参阅 MSDN 库中的[单元测试代码](../test/unit-test-your-code.md)。

## <a name="BKMK_In_this_topic"></a> 在本主题中
 [单元测试框架和测试项目](#BKMK_Unit_test_frameworks_and_test_projects)

 [在测试资源管理器中运行测试](#BKMK_Running_tests_in_Test_Explorer)

- [运行测试](#BKMK_Running_tests)

  [查看测试结果](#BKMK_Viewing_test_results)

- [查看测试详细信息](#BKMK_Viewing_test_details)

- [查看测试方法的源代码](#BKMK_Viewing_the_source_code_of_a_test_method)

  [组织测试列表](#BKMK_Organizing_the_test_list)

- [对测试进行分组](#BKMK_Grouping_tests)

- [搜索和筛选测试列表](#BKMK_Searching_and_filtering_the_test_list)

  [调试单元测试](#BKMK_Debugging_unit_tests)

## <a name="BKMK_Unit_test_frameworks_and_test_projects"></a> 单元测试框架和测试项目
 适用于 Windows 应用商店应用的 Visual Studio Express 包括针对托管和本机 C++ 代码的 Microsoft 单元测试框架。 测试资源管理器可从解决方案的多个测试项目以及从作为生产代码项目的一部分的测试类中运行测试。 测试项目可以是 Visual C++ 或 Visual C# 与 Visual Basic 单元测试框架的任意组合。 当测试中的代码针对 .NET Framework 进行编写时，无论目标代码使用何种语言，均可使用任何 .NET Framework 语言编写测试项目。 本机 C/C++ 代码项目必须使用 C++ 单元测试框架进行测试。

## <a name="BKMK_Running_tests_in_Test_Explorer"></a> 在测试资源管理器中运行测试
 在生成测试项目时，测试将出现在测试资源管理器中。 如果测试资源管理器不可见，请选择 Visual Studio 菜单上的“测试”  ，然后依次选择“Windows” 、“测试资源管理器” 。

 ![单元测试资源管理器](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

 当你运行、编写以及重新运行测试时，测试资源管理器将在 **“失败的测试”**、 **“通过的测试”**、 **“跳过的测试”** 和 **“未运行的测试”** 默认组中显示结果。 你可以更改测试资源管理器对测试进行分组的方式。

 可以从测试资源管理器的工具栏执行查找、组织和运行测试等大部分工作。

 ![从测试资源管理器工具栏运行测试](../test/media/ute-toolbar.png "UTE_ToolBar")

### <a name="BKMK_Running_tests"></a> 运行测试
 你可以运行解决方案中的所有测试、组中的所有测试或你选择的一组测试。 执行下列操作之一：

- 若要运行解决方案中的所有测试，请选择 **“全部运行”**。

- 若要运行默认组中的所有测试，请选择 **“运行...”** ，然后选择菜单上的组。

- 选择想要运行的各个测试，打开选定测试的快捷菜单，然后选择“运行选定测试”。

  测试运行时，测试资源管理器窗口顶部的“通过/失败”条动态显示。 测试运行结束时，如果所有测试均通过，则“通过/失败”条将变为绿色；如果有测试失败，则变为红色。

## <a name="BKMK_Viewing_test_results"></a> 查看测试结果
 当你运行、编写以及重新运行测试时，测试资源管理器将在 **“失败的测试”**、 **“通过的测试”**、 **“跳过的测试”** 和 **“未运行的测试”** 组中显示结果。 测试运行的摘要显示在测试资源管理器底部的细节窗格中。

### <a name="BKMK_Viewing_test_details"></a> 查看测试详细信息
 若要查看单个测试的详细信息，请选择该测试。

 测试细节窗格中显示以下信息：

- 源文件名和测试方法的行号。

- 测试的状态。

- 运行测试方法所花的时间。

  如果测试失败，细节窗格中还将显示：

- 测试的单元测试框架返回的消息。

- 测试失败时的堆栈跟踪。

### <a name="BKMK_Viewing_the_source_code_of_a_test_method"></a> 查看测试方法的源代码
 若要在 Visual Studio 编辑器中显示测试方法的源代码，请选择该测试，然后在快捷菜单上选择“打开测试”（键盘：F12）。

## <a name="BKMK_Organizing_the_test_list"></a> 组织测试列表

### <a name="BKMK_Grouping_tests"></a> 对测试进行分组
 默认情况下，测试资源管理器将测试显示为“失败的测试”、“通过的测试”、“跳过的测试”和“未运行的测试”的子节点。

|||
|-|-|
|![测试资源管理器的分组按钮](../test/media/ute-groupby-btn.png "UTE_GroupBy_btn")|若要按执行它们所花的时间对测试进行分组，请打开“分组方式”列表并选择“持续时间”。 选择“测试结果”以切换到原始分组。|

### <a name="BKMK_Searching_and_filtering_the_test_list"></a>搜索和筛选测试列表
 当有大量的测试时，可在测试资源管理器搜索框中键入指定的字符串，以按该字符串筛选列表。 在输入搜索字符串之前，可以通过从筛选器列表中进行选择来将筛选器限制为特定类型的字符串。

 ![搜索筛选器类别](../test/media/ute-searchfilter.png "UTE_SearchFilter")

## <a name="BKMK_Debugging_unit_tests"></a> 调试单元测试
 可以使用测试资源管理器为你的测试启动调试会话。 使用 Visual Studio 调试程序无缝地逐句通过代码将使你在单元测试和所测试项目之间来回反复。 若要开始调试：

1. 在 Visual Studio 编辑器中，在想要调试的一个或多个测试方法中设置断点。

   > [!NOTE]
   > 因为测试方法可以按任何顺序运行，请在想要调试的所有测试方法中设置断点。

2. 在测试资源管理器中，选择测试方法，然后选择快捷菜单上的“调试选定的测试”。

   有关该调试器的详细信息，请参阅 [Debugging in Visual Studio](../debugger/debugging-in-visual-studio.md)。
