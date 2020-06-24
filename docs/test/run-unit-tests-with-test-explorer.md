---
title: 使用测试资源管理器运行和调试单元测试
description: 了解如何使用测试资源管理器在 Visual Studio 中运行测试。 本主题介绍如何启用生成后自动测试运行、查看测试结果、对测试列表进行分组和筛选、创建播放列表、调试测试以及使用测试快捷方式。
ms.date: 07/29/2019
ms.topic: how-to
f1_keywords:
- vs.unittesting.testexplorer.overview
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6de463fbc941273bed9b949958b9463be6ea1fa3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285629"
---
# <a name="run-unit-tests-with-test-explorer"></a>使用测试资源管理器运行单元测试

使用测试资源管理器从 Visual Studio 或第三方单元测试项目运行单元测试。 还可以使用测试资源管理器将测试分组到不同类别、筛选测试列表以及创建、保存和运行测试播放列表。 可以调试测试并分析测试性能和代码覆盖率。

Visual Studio 包含适用于托管和本机代码的 Microsoft 单元测试框架。 但是，测试资源管理器还可以运行任何单元测试框架，只要该框架实现了测试资源管理器适配器。 若要详细了解如何安装第三方单元测试框架，请参阅[安装第三方单元测试框架](../test/install-third-party-unit-test-frameworks.md)

测试资源管理器可从解决方案的多个测试项目以及生产代码项目包含的测试类中运行测试。 测试项目可以使用不同的单元测试框架。 如果待测试的代码是为 .NET 编写的，则可以面向 .NET 的任何语言编写测试项目，而不考虑目标代码的语言。 本机 C/C++ 代码项目必须使用 C++ 单元测试框架进行测试。 有关详细信息，请参阅[编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)。

## <a name="run-tests-in-test-explorer"></a>在测试资源管理器中运行测试

在[生成测试项目](../test/getting-started-with-unit-testing.md)时，测试将出现在“测试资源管理器”中。 如果测试资源管理器不可见，请选择 Visual Studio 菜单上的“测试”  ，然后依次选择“Windows” 、“测试资源管理器” 。

::: moniker range="vs-2017"
![单元测试资源管理器](../test/media/ute_failedpassednotrunsummary.png)
::: moniker-end
::: moniker range=">=vs-2019"
![测试资源管理器](../test/media/vs-2019/test-explorer-16-2.png)
::: moniker-end

::: moniker range="vs-2017"
当你运行、编写以及重新运行测试时，测试资源管理器将在 **“失败的测试”** 、 **“通过的测试”** 、 **“跳过的测试”** 和 **“未运行的测试”** 默认组中显示结果。 你可以更改测试资源管理器对测试进行分组的方式。
::: moniker-end
::: moniker range=">=vs-2019"
当你运行、编写以及重新运行测试时，测试资源管理器将在“项目”、“命名空间”和“类”默认分组中显示结果  。 你可以更改测试资源管理器对测试进行分组的方式。
::: moniker-end

可从测试资源管理器的工具栏执行查找、组织和运行测试等大部分工作。

::: moniker range="vs-2017"
![从测试资源管理器工具栏运行测试](../test/media/ute_toolbar.png)
::: moniker-end
::: moniker range=">=vs-2019"
![从测试资源管理器工具栏运行测试](../test/media/vs-2019/test-explorer-toolbar-diagram-16-2.png)
::: moniker-end

### <a name="run-tests"></a>运行测试

::: moniker range="vs-2017"
你可以运行解决方案中的所有测试、组中的所有测试或你选择的一组测试。 执行下列操作之一：

- 若要运行解决方案中的所有测试，请选择 **“全部运行”** 。

- 若要运行默认组中的所有测试，请选择“运行”，然后选择菜单上的组。

- 选择要运行的各个测试，打开选定测试的右键单击菜单，再选择“运行选定测试”。

- 如果各个测试没有防止其以任何顺序运行的依赖项，则可使用工具栏上的 ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) 切换按钮来打开并行测试执行。 这可以显著降低运行所有测试所需的时间。

测试运行时，测试资源管理器窗口顶部的“通过/失败”条将动态显示 。 测试运行结束时，如果所有测试均通过，则“通过/失败”条将变为绿色；如果有测试失败，则变为红色。
::: moniker-end
::: moniker range=">=vs-2019"
你可以运行解决方案中的所有测试、组中的所有测试或你选择的一组测试。 执行下列操作之一：

- 若要运行解决方案中的所有测试，请选择“全部运行”图标。

- 若要运行默认组中的所有测试，请选择“运行”图标，然后选择菜单上的组。

- 选择要运行的各个测试，打开选定测试的右键单击菜单，再选择“运行选定测试”。

- 如果各个测试没有阻止其以任何顺序运行的依赖项，则可以在工具栏的设置菜单中启用并行测试执行。 这可以显著降低运行所有测试所需的时间。
::: moniker-end

### <a name="run-tests-after-every-build"></a>每次生成后运行测试
::: moniker range="vs-2017"
|Button|描述|
|-|-|
|![生成后运行](../test/media/ute_runafterbuild_btn.png)|要在每个本地生成后运行单元测试，请在标准菜单上选择“测试”，然后在测试资源管理器的工具栏上选择“生成后运行测试”  。|

> [!NOTE]
> 在每次生成后运行单元测试需要 Visual Studio 2017 Enterprise 或 Visual Studio 2019。 对于 Visual Studio 2019，它包含在 Community、Professional 和 Enterprise 中。
::: moniker-end
::: moniker range=">=vs-2019"
若要在每个本地生成后运行单元测试，请在“测试资源管理器”工具栏中打开设置图标并选择“生成后运行测试”。
::: moniker-end

## <a name="view-test-results"></a>查看测试结果

当你运行、编写以及重新运行测试时，测试资源管理器将在 **“失败的测试”** 、 **“通过的测试”** 、 **“跳过的测试”** 和 **“未运行的测试”** 组中显示结果。 测试运行的摘要显示在测试资源管理器底部或侧面的细节窗格中。

### <a name="view-test-details"></a>查看测试详细信息

若要查看单个测试的详细信息，请选择该测试。

::: moniker range="vs-2017"
![测试执行详细信息](../test/media/ute_testdetails.png)
::: moniker-end
::: moniker range=">=vs-2019"
![测试执行详细信息](../test/media/vs-2019/test-explorer-detail.png)
::: moniker-end

测试细节窗格中显示以下信息：

- 源文件名和测试方法的行号。

- 测试的状态。

- 运行测试方法所花的时间。

如果测试失败，细节窗格中还将显示：

- 测试的单元测试框架返回的消息。

- 测试失败时的堆栈跟踪。

### <a name="view-the-source-code-of-a-test-method"></a>查看测试方法的源代码

若要在 Visual Studio 编辑器中显示测试方法的源代码，请依次选择测试和右键单击菜单中的“打开测试”（键盘快捷键：**F12**）。

## <a name="group-and-filter-the-test-list"></a>分组和筛选测试列表

通过测试资源管理器，可以将测试分组到预定义类别中。 在测试资源管理器中运行的大多数单元测试框架允许你定义自己的类别和类别/值对，以便对测试进行分组。 此外还可以通过匹配字符串和测试属性来筛选测试列表。

### <a name="group-tests-in-the-test-list"></a>在测试列表中的测试进行分组

::: moniker range="vs-2017"
若要更改测试的组织方式，请依次选择“分组依据”按钮 ![测试资源管理器的分组按钮](../test/media/ute_groupby_btn.png) 旁边的向下箭头和新分组条件。

![在测试资源管理器中按类别对测试分组](../test/media/ute_groupbycategory.png)
::: moniker-end
::: moniker range=">=vs-2019"
通过测试资源管理器，可以将测试分组到层次结构中。 默认层次结构分组包括“项目”、“命名空间”和“类”  。 若要更改测试的组织方式，请依次选择“分组依据”按钮 ![测试资源管理器的分组按钮](../test/media/ute_groupby_btn.png) 和新分组条件。

![在测试资源管理器中按类别对测试分组](../test/media/vs-2019/test-explorer-groupby-162.png)

你可以定义自己的层次结构级别，然后通过按喜欢的顺序选择“分组依据”选项来依次按“状态”和“类”进行分组 。

![依次按“状态”和“类”分组](../test/media/vs-2019/test-explorer-groupby-state-16-2.png)
::: moniker-end

### <a name="test-explorer-groups"></a>测试资源管理器组

::: moniker range="vs-2017"
|Group|描述|
|-|-----------------|
|**持续时间**|按执行时间对测试进行分组：快速、中等和慢速  。|
|**结果**|按执行结果对测试进行分组：失败的测试、跳过的测试和通过的测试  。|
|**特征**|按你定义的类别/值对对测试进行分组。 用于指定特征类别和值的语法由单元测试框架定义。|
|**Project**|按项目名称对测试进行分组。|
::: moniker-end
::: moniker range=">=vs-2019"
|Group|描述|
|-|-----------------|
|**持续时间**|按执行时间对测试进行分组：快速、中等和慢速  。|
|**状态**|按执行结果对测试进行分组：失败的测试、跳过的测试、通过的测试和未运行的测试   |
|**目标框架** | 按项目目标框架对测试进行分组 |
|**命名空间**|按包含命名空间对测试进行分组。|
|**Project**|按包含项目对测试进行分组。|
|**类**|按包含类对测试进行分组。|
::: moniker-end

### <a name="traits"></a>Traits

特征通常是类别名称/值对，但也可以是单个类别。 特性可以分配给由单元测试框架标识为测试方法的方法。 单元测试框架可以定义特征类别。 你可以向特征类别添加值，以便定义自己的类别名称/值对。 用于指定特征类别和值的语法由单元测试框架定义。

**适用于托管代码的 Microsoft 单元测试框架中的特征**

在适用于托管应用的 Microsoft 单元测试框架中，在  <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute> 属性中定义特征名称/值对。 测试框架还包括以下预定义特征：

|特征|描述|
|-|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>|“所有者”类别由单元测试框架定义，并要求你提供所有者的字符串值。|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>|“优先级”类别由单元测试框架定义，并要求你提供优先级的整数值。|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCategoryAttribute>|你可以通过 TestCategory 属性提供类别而不提供值。|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>|你可以通过 TestProperty 属性定义特征类别/值对。|


**适用于 C++ 的 Microsoft 单元测试框架中的特征**

请参阅[如何使用适用于 C++ 的 Microsoft 单元测试框架](how-to-use-microsoft-test-framework-for-cpp.md)。

## <a name="create-custom-playlists"></a>创建自定义播放列表

::: moniker range="vs-2017"
你可以创建和保存想要作为组运行或查看的测试列表。 选择播放列表时，列表中的测试将显示在测试资源管理器中。 你可以将一个测试添加到多个播放列表，并且当你选择默认的 **“所有测试”** 播放列表时，项目中的所有测试都可用。

![选择播放列表](../test/media/ute_playlist.png)

**若要创建播放列表**，请在测试资源管理器中选择一个或多个测试。 在右键单击菜单中，依次选择“添加到播放列表” > “NewPlaylist”。 保存具有该名称的文件，并定位到你在 **“创建新的播放列表”** 对话框中指定的位置。

**若要将测试添加到播放列表**，请在测试资源管理器中选择一个或多个测试。 在右键单击菜单中，依次选择“添加到播放列表”和要将测试添加到的播放列表。

若要打开播放列表，请从 Visual Studio 菜单中选择“测试”>“播放列表”，然后从“最近使用的播放列表”列表中选择，或选择“打开播放列表”以指定播放列表的名称和位置。

如果各个测试没有防止其以任何顺序运行的依赖项，则可使用工具栏上的 ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) 切换按钮来打开并行测试执行。 这可以显著降低运行所有测试所需的时间。
::: moniker-end
::: moniker range=">=vs-2019"
你可以创建和保存想要作为组运行或查看的测试列表。 选择播放列表时，列表中的测试将显示在新的“测试资源管理器”选项卡中。可以将一个测试添加到多个播放列表中。

**若要创建播放列表**，请在测试资源管理器中选择一个或多个测试。 在右键单击菜单中，依次选择“添加到播放列表” > “新建播放列表” 。

![创建播放列表](../test/media/vs-2019/test-explorer-playlist-16-2.png)

此时将在新的“测试资源管理器”选项卡中打开播放列表。可以使用此播放列表一次，然后将其丢弃，也可以单击播放列表窗口工具栏中的“保存”按钮，然后选择要保存播放列表的名称和位置。

![在单独的“测试资源管理器”选项卡中打开播放列表](../test/media/vs-2019/test-explorer-playlist-tab-16-2.png)

**若要创建播放列表**，请在测试资源管理器中选择一个或多个测试。 右键单击并选择“添加到播放列表” > “新建播放列表” 。

若要打开播放列表，请选择 Visual Studio 工具栏中的播放列表图标，然后从菜单中选择以前保存的播放列表文件。
::: moniker-end

::: moniker range=">=vs-2019"
### <a name="test-explorer-columns"></a>测试资源管理器列

除了特征、堆栈跟踪、错误消息和完全限定名以外，[组](#test-explorer-groups)也可用作测试资源管理器中的列。 默认情况下，大多数列不可见，你可以自定义要显示的列及其显示顺序。

![依次按“状态”和“类”分组](../test/media/vs-2019/test-explorer-columns-16-2.png)

### <a name="filter-sort-and-rearrange-test-columns"></a>对测试列进行筛选、排序和重新排列

可以对列进行筛选、排序和重新排列。
* 若要筛选到特定特征，请单击“特征”列顶部的“筛选器”图标。

  ![列筛选器](../test/media/vs-2019/test-explorer-filter-column-16-2.png)

* 若要更改列的顺序，请单击列标题并将其向左或向右拖动。

* 若要对列进行排序，请单击列标题。 并非所有列都可以进行排序。 还可通过按住 Shift 并单击其他列标头来按辅助列进行排序。

  ![列排序](../test/media/vs-2019/test-explorer-sort-column-16-2.png)
::: moniker-end

## <a name="search-and-filter-the-test-list"></a>搜索和筛选测试列表

你还可以使用测试资源管理器搜索筛选器来限制你所查看和运行项目中的测试方法。

在测试资源管理器的搜索框中键入字符串并选择 Enter 时，测试列表将筛选为仅显示包含该字符串的完全限定名的测试 。

按其他条件进行筛选：

1. 打开搜索框右侧的下拉列表。

2. 选择新条件。

3. 在引号中输入筛选值。 如果要在字符串上搜索完全匹配，而不是包含匹配，请使用等于号 (=) 而不是冒号 (:)。

::: moniker range="vs-2017"
![在测试资源管理器中筛选测试](../test/media/ute_filtertestlist.png)
::: moniker-end
::: moniker range=">=vs-2019"
![在测试资源管理器中筛选测试](../test/media/vs-2019/test-explorer-search-filter-16-2.png)
::: moniker-end

> [!NOTE]
> 搜索不区分大小，并将指定字符串与条件值的任何部分匹配。

::: moniker range="vs-2017"
|限定符|描述|
|-|-----------------|
|**特征**|搜索特征类别和值的匹配项。 用于指定特征类别和值的语法由单元测试框架定义。|
|**Project**|搜索测试项目名称的匹配项。|
|**错误消息**|搜索由失败的断言返回的用户定义错误消息的匹配项。|
|**文件路径**|搜索测试源文件的完全限定文件名的匹配项。|
|**完全限定名**|搜索测试命名空间、类和方法的完全限定名的匹配项。|
|**输出**|搜索写入标准输出 (stdout) 或标准错误 (stderr) 的用户定义错误消息。 用于指定输出消息的语法由单元测试框架定义。|
|**结果**|搜索“测试资源管理器”类别名中的匹配项：失败的测试、跳过的测试和通过的测试  。|
::: moniker-end
::: moniker range=">=vs-2019"
|限定符|描述|
|-|-----------------|
|**状态**|搜索“测试资源管理器”类别名中的匹配项：失败的测试、跳过的测试和通过的测试  。|
|**特征**|搜索特征类别和值的匹配项。 用于指定特征类别和值的语法由单元测试框架定义。|
|**完全限定名**|搜索测试命名空间、类和方法的完全限定名的匹配项。|
|**Project**|搜索测试项目名称的匹配项。|
|**目标框架**|搜索“测试资源管理器”类别名中的匹配项：失败的测试、跳过的测试和通过的测试  。|
|**命名空间**|搜索测试命名空间的匹配项。|
|**类**|搜索测试类名的匹配项。|
::: moniker-end

若要排除筛选结果的一个子集，请使用以下语法：

```
FilterName:"Criteria" -FilterName:"SubsetCriteria"
```

例如，`FullName:"MyClass" - FullName:"PerfTest"` 返回名称中包含“MyClass”的所有测试，名称中包含“PerfTest”的测试除外。

## <a name="debug-and-analyze-unit-tests"></a>调试并分析单元测试

可以使用测试资源管理器为你的测试启动调试会话。 使用 Visual Studio 调试程序无缝地逐句通过代码将使你在单元测试和所测试项目之间来回反复。 若要开始调试：

1. 在 Visual Studio 编辑器中，在想要调试的一个或多个测试方法中设置断点。

    > [!NOTE]
    > 因为测试方法可以按任何顺序运行，请在你想要调试的所有测试方法中设置断点。

2. 在测试资源管理器中，依次选择测试方法和右键单击菜单中的“调试选定测试”。

   有关该调试程序的详细信息，请参阅[在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md)。

### <a name="diagnose-test-method-performance-issues"></a>诊断测试方法性能问题

若要诊断测试方法为何花费过多时间，请在测试资源管理器中依次选择方法和右键单击菜单中的“配置文件选定测试”。 请参阅[检测分析报告](../profiling/understanding-instrumentation-data-values.md?view=vs-2017)。

### <a name="analyze-unit-test-code-coverage"></a>分析单元测试代码覆盖率

可以使用 Visual Studio Enterprise 版本中提供的 Visual Studio 代码覆盖率工具确定你的单元测试实际测试的产品代码量。 你可以在选定的测试上或解决方案中的所有测试上运行代码覆盖率。

在解决方案中为测试方法运行代码覆盖率：

::: moniker range="vs-2017"

1. 在顶部菜单栏上选择“测试”，然后选择“分析代码覆盖率” 。

2. 从子菜单中选择下列命令之一：

    - **选定的测试** 运行你在测试资源管理器中选择的测试方法。

    - **所有测试** 在解决方案中运行所有测试方法。

::: moniker-end

::: moniker range=">=vs-2019"

* 在测试资源管理器中单击鼠标右键，然后选择“分析所选测试的代码覆盖率”

::: moniker-end

“代码覆盖率结果”窗口显示行、函数、类、命名空间和模块执行的产品代码块的百分比。

有关详细信息，请参阅[使用代码覆盖率确定正在测试的代码数量](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)。

## <a name="test-shortcuts"></a>测试快捷方式

可以从“测试资源管理器”运行测试，方法是：在代码编辑器中右键单击测试，并选择“运行测试”，或者在 Visual Studio 中使用默认的[测试资源管理器快捷方式](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL)。 一些快捷方式是基于上下文的。 这意味着它们根据光标在代码编辑器中的位置来运行或调试测试。 如果光标位于某一测试方法内，则运行该测试方法。 如果光标位于类级别，则运行该类中的所有测试。 如果光标位于命名空间级别，则运行该命名空间级别中的所有测试。

|常见命令| 键盘快捷键|
|-|------------------------|
|测试资源管理器.调试上下文中的所有测试|Ctrl+R、Ctrl+T   |
|测试资源管理器.运行上下文中的所有测试|Ctrl+R、T  |
|测试资源管理器.运行所有测试|Ctrl+R、A|
|测试资源管理器.重复上次运行|Ctrl+R、L|

> [!NOTE]
> 无法运行抽象类中的测试，因为仅在抽象类中定义测试，但未实例化。 若要运行抽象类中的测试，请创建派生自该抽象类的类。

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
- [将单元测试作为 64 位进程运行](../test/run-a-unit-test-as-a-64-bit-process.md)
- [测试资源管理器常见问题解答](test-explorer-faq.md)
