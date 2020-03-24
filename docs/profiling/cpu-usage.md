---
title: 分析 CPU 使用率 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2018
ms.topic: conceptual
ms.assetid: 7501a20d-04a1-480f-a69c-201524aa709d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 351247f50560896d53267fcf8d7f4a66a81b9461
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62553433"
---
# <a name="analyze-cpu-usage"></a>分析 CPU 使用情况

开始调查应用中的性能问题的好方法之一是了解其 CPU 使用情况。 “CPU 使用情况”性能工具显示 C++、C#/Visual Basic 以及 JavaScript 应用中执行代码所花费的 CPU 时间和百分比  。

“CPU 使用情况”工具可以在打开的 Visual Studio 项目、在已安装的 Microsoft Store 应用上运行，也可以附加到正在运行的应用或进程  。 可以在本地或远程计算机运行该工具，也可以在模拟器或仿真器上运行该工具。 有关详细信息，请参阅[运行带或不带调试器的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)。

无论是否进行调试，都可以运行“CPU 使用情况”工具  。 在调试器中，可以打开和关闭 CPU 分析，并查看 CPU 使用情况的每个细分功能。 可以在暂停执行时（例如在断点处）查看 CPU 使用情况结果。

以下说明介绍如何使用不带调试器的“CPU 使用情况”工具以及 Visual Studio“性能探查器”   。 示例使用本地计算机上的发布版本。 发布版本提供了实际应用性能的最佳视图。 要使用调试版本分析 CPU 使用情况，请参阅[性能分析初学者指南](../profiling/beginners-guide-to-performance-profiling.md)。

通常，本地计算机最好复制已安装的应用执行。 对于 Windows Phone 应用，直接从设备收集数据这种方式提供的数据最准确。 要从远程设备收集数据，请直接在该设备上运行应用，而不通过使用远程桌面连接运行。

>[!NOTE]
>需要 Windows 7 或更高版本才能使用[性能探查器](../profiling/profiling-feature-tour.md)。

## <a name="collect-cpu-usage-data"></a>收集 CPU 使用量数据

1. 在 Visual Studio 项目中，将解决方案配置设置为“发布”，然后选择“本地计算机”作为部署目标   。

    ![选择“版本”和“本地计算机”](../profiling/media/cpuuse_selectreleaselocalmachine.png "选择“版本”和“本地计算机”")

1. 选择“调试” > “性能探查器”   。

1. 在“可用工具”下，选择“CPU 使用情况”，然后选择“启动”    。

    ![选择“CPU 使用率”](../profiling/media/cpuuse_lib_choosecpuusage.png "选择“CPU 使用率”")

4. 应用启动后，诊断会话即会开始，并显示 CPU 使用情况数据。 完成收集数据后，选择“停止收集”  。

   ![停止 CPU 使用量数据收集](../profiling/media/cpu_use_wt_stopcollection.png "停止 CPU 使用量数据收集")

   CPU 使用量工具可分析数据并显示报告。

   ![CPU 使用率报告](../profiling/media/cpu_use_wt_report.png "CPU 使用率报告")

## <a name="analyze-the-cpu-usage-report"></a>分析 CPU 使用量报告

诊断报表按“CPU 总量”从最高到最低进行排序  。 通过选择列标题更改排序顺序或排序列。 使用“筛选器”下拉列表以选择或取消选择要显示的线程，并使用“搜索”框搜索特定线程或节点   。

::: moniker range=">=vs-2019"
从 Visual Studio 2019 开始，可以单击“展开热路径”  和“显示热路径”  按钮，以查看树视图中使用最高 CPU 百分比的函数调用。
::: moniker-end

### <a name="cpu-usage-data-columns"></a><a name="BKMK_Call_tree_data_columns"></a> CPU 使用情况数据列

|||
|-|-|
|CPU 总量 [单位，以百分数计算] |![总数据量 % 等式](../profiling/media/cpu_use_wt_totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> 调用函数所使用的毫秒数和 CPU 百分比，以及函数在所选时间范围内调用的函数。 这与“CPU 利用率”时间线图不同，后者是将时间范围内的 CPU 总活动量与可用 CPU 总量进行比较  。|
|自 CPU [单位，以百分数计算] |![自测 % 等式](../profiling/media/cpu_use_wt_selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> 在所选时间范围内调用函数所使用的毫秒数和 CPU 百分比，不包括函数调用的函数。|
|**模块**|包含函数的模块的名称。

### <a name="the-cpu-usage-call-tree"></a><a name="BKMK_The_CPU_Usage_call_tree"></a> CPU 使用率调用关系树

要查看调用关系树，请选择报表中的父节点。 “CPU 使用情况”页面将打开“调用方/被调用方”视图   。 在“当前视图”下拉列表中，选择“调用树”   。

#### <a name="call-tree-structure"></a><a name="BKMK_Call_tree_structure"></a>调用关系树结构

::: moniker range=">=vs-2019"
![调用树结构](../profiling/media/vs-2019/cpu-use-wt-getmaxnumbercalltree-annotated.png "调用关系树结构")
::: moniker-end
::: moniker range="vs-2017"
![调用树结构](../profiling/media/cpu_use_wt_getmaxnumbercalltree_annotated.png "调用关系树结构")
::: moniker-end

|||
|-|-|
|![步骤 1](../profiling/media/procguid_1.png "ProcGuid_1")|CPU 使用情况调用树中的顶级节点是一个伪节点。|
|![步骤 2](../profiling/media/procguid_2.png "ProcGuid_2")|在大多数应用中，当“显示外部代码”选项处于禁用状态时，第二级别节点就是“[外部代码]”节点   。 该节点包含启动和停止应用、绘制 UI、控制线程计划以及向应用提供其他低级别服务的系统和框架代码。|
|![步骤 3](../profiling/media/procguid_3.png "ProcGuid_3")|二级节点的子级为用户代码方法和异步例程，它们由二级系统和框架代码进行调用或创建。|
|![步骤 4](../profiling/media/procguid_4.png "ProcGuid_4")|方法的子节点仅有父方法调用的数据。 禁用“显示外部代码”  后，应用方法只能包含 **[外部代码]** 节点。|

#### <a name="external-code"></a><a name="BKMK_External_Code"></a> 外部代码

由代码执行的系统和框架函数称为“外部代码”  。 外部代码函数启动和停止应用、绘制 UI、控制线程以及向应用提供其他低级别服务。 在大多数情况下，你不会对外部代码感兴趣，因此 CPU 使用情况调用树可将用户方法的外部函数收集到一个“[外部代码]”节点中  。

要查看外部代码的调用路径，请在主诊断报表页面（右窗格）上的“筛选器”下拉列表中选择“显示外部代码”，然后选择“应用”    。 “CPU 使用情况”页面的“调用树”视图随即展开外部代码调用   。 （“筛选器”下拉菜单在主诊断页面上可用，在详细视图上不可用。  ）

![显示外部代码](../profiling/media/cpu_use_wt_filterview.png "显示外部代码")

许多外部代码调用链都是深度嵌套的，因此链的宽度可能超过“函数名”列的显示宽度  。 函数名则显示为“...”  。

![调用树中嵌套的外部代码](../profiling/media/cpu_use_wt_showexternalcodetoowide.png "调用树中嵌套的外部代码")

要查找所需的函数名称，请使用搜索框。 将鼠标悬停在所选行上或使用水平滚动条来查看数据。

::: moniker range=">=vs-2019"
![搜索嵌套的外部代码](../profiling/media/vs-2019/cpu-use-wt-showexternalcodetoowide-found.png "搜索嵌套的外部代码")
::: moniker-end
::: moniker range="vs-2017"
![搜索嵌套的外部代码](../profiling/media/cpu_use_wt_showexternalcodetoowide_found.png "搜索嵌套的外部代码")
::: moniker-end

### <a name="asynchronous-functions-in-the-cpu-usage-call-tree"></a><a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a> CPU 使用情况调用树中的异步函数

 当编译器遇到异步方法时，它会创建一个隐藏的类来控制方法的执行。 从概念上讲，此类是状态机。 该类具有编译器生成的异步调用原始方法以及运行其所需的回调、计划程序和迭代器的函数。 当父方法调用原始方法时，编译器将从父方法的执行上下文中删除该方法，并在控制应用执行的系统和框架代码的上下文中运行隐藏的类方法。 异步方法通常（但不总是）在一个或多个不同线程上执行。 此代码在“CPU 使用情况”调用树中显示为“[外部代码]”节点的子节点，位于树的顶部节点下面   。

在以下示例中，“[外部代码]”下方的前两个节点是编译器生成的状态机类的方法  。 第三个节点是对原始方法的调用。

![异步节点](media/cpu_use_wt_getmaxnumberasync_selected.png "异步节点")

展开生成的方法，以显示正在进行的操作：

![展开的异步节点](media/cpu_use_wt_getmaxnumberasync_expandedcalltree.png "展开的异步节点")

- `MainPage::GetMaxNumberAsyncButton_Click` 只管理任务值列表、计算结果最大值以及显示输出。

- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` 显示用于计划和启动 48 个任务所需的活动，这些任务将包装对 `GetNumberAsync`的调用。

- `MainPage::<GetNumberAsync>b__b` 显示调用 `GetNumber` 的任务的活动。
