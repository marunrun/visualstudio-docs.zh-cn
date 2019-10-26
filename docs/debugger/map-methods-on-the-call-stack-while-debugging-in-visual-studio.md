---
title: 创建调用堆栈的可视地图 |Microsoft Docs
ms.date: 11/26/2018
ms.topic: conceptual
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- call stacks, code maps
- Call Stack window, mapping calls
- debugging [Visual Studio], diagramming the call stack
- call stacks, mapping
- Call Stack window, visualizing
- debugging code visually
- debugging [Visual Studio], mapping the call stack
- call stacks, visualizing
- debugging, code maps
- Call Stack window, tracing calls visually
- Call Stack window, show on code map
- debugging [Visual Studio], tracing the call stack visually
- debugging [Visual Studio], visualizing the call stack
ms.assetid: d6a72e5e-f88d-46fc-94a3-1789d34805ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 135c7c66c9c6602f8c2e32bbdc1ba6e2fd28f548
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911522"
---
# <a name="create-a-visual-map-of-the-call-stack-while-debugging-c-visual-basic-c-javascript"></a>调试时创建调用堆栈的可视地图（C#、Visual Basic、 C++、JavaScript）

创建代码映射，以便在调试时对调用堆栈进行可视化跟踪。 可以在映射中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

有关演练，请观看此视频：[视频：直观地调试与代码图调试器集成 (通道 9)](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

有关可用于代码映射的命令和操作的详细信息，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

>[!IMPORTANT]
>只能在[Visual Studio Enterprise 版本](https://visualstudio.microsoft.com/downloads)中创建代码图。

下面简要介绍代码图：

 ![用代码图上的调用堆栈进行调试](../debugger/media/debuggermap_overview.png "DebuggerMap_Overview")

## <a name="MapStack"></a>映射调用堆栈

1. 在C#Visual Studio Enterprise、Visual Basic、 C++或 JavaScript 项目中，通过选择 "**调试**" > "**启动调试**" 或按**F5**来启动调试。

1. 在应用进入中断模式或单步执行函数后，选择 "**调试**" > **代码图**，或按**Ctrl**+**Shift**+ **`** 。

   当前的调用堆栈在新代码图上显示为橙色：

   ![请参阅代码图上的调用堆栈](../debugger/media/debuggermap_seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

当你继续调试时，代码图会自动更新。 更改地图项或布局不会对代码造成任何影响。 你可随意在图上重命名、移动或移除任何内容。

若要获取有关项的详细信息，请将鼠标悬停在该项上，并查看项的工具提示。 还可以在工具栏中选择 "**图例**" 以了解每个图标的含义。

![代码图图例](../debugger/media/debuggermap_showlegend.png "代码图图例")

>[!NOTE]
>**关系图可能基于代码图顶部代码的较旧版本**的消息表示，代码可能在你上次更新映射后发生了更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

## <a name="map-external-code"></a>映射外部代码

默认情况下，只有你自己的代码会显示在图中。 查看地图上的外部代码：

- 右键单击 "**调用堆栈**" 窗口，然后选择 "**显示外部代码**"：

  ![使用 "调用堆栈" 窗口显示外部代码](../debugger/media/debuggermap_callstackmenu.png "DebuggerMap_CallStackMenu")
- 或者取消选中 "在 Visual Studio**工具**中**启用仅我的代码**（或**调试**）" >**选项** > **调试**：

  ![使用 "选项" 对话框显示外部代码](../debugger/media/debuggermap_debugoptions.png "DebuggerMap_DebugOptions")

## <a name="control-the-maps-layout"></a>控制地图的布局

更改地图的布局不会对代码造成任何影响。

若要控制地图的布局，请选择地图工具栏上的 "**布局**" 菜单。

在 "**布局**" 菜单中，可以：

- 更改默认布局。
- 停止自动重新排列映射，方法是**在调试时**取消选择 "自动布局"。
- 通过取消选择**增量布局**来添加项时尽可能少地重新排列映射。

## <a name="MakeNotes"></a>对代码进行标注

您可以添加注释以跟踪代码发生的情况。

若要添加注释，请在代码图中右键单击，然后选择 "**编辑**" > "**新建注释**"，然后键入注释。

若要在注释中添加新行，请按**Shift**+**enter**。

 ![向代码图上的调用堆栈添加注释](../debugger/media/debuggermap_addcomment.png "DebuggerMap_AddComment")

## <a name="UpdateMap"></a>使用下一个调用堆栈更新映射

当你运行应用程序到下一个断点或单步执行函数时，映射会自动添加新的调用堆栈。

![用下一个调用堆栈更新代码图](../debugger/media/debuggermap_addclearcallstack.png "DebuggerMap_AddClearCallStack")

若要停止映射自动添加新的调用堆栈，请在代码图工具栏上选择 "![在代码图上自动显示调用堆栈](../debugger/media/debuggermap_automaticupdateicon.gif "自动在代码图上显示调用堆栈")"。 该映射将继续突出显示现有调用堆栈。 若要手动将当前调用堆栈添加到地图中，请按**Ctrl**+**Shift**+ **`** "。

## <a name="AddRelatedCode"></a>向映射添加相关代码

现在，你已获得了一个地图， C#在或 Visual Basic 中，你可以添加诸如字段、属性和其他方法等项，以跟踪代码中发生的情况。

若要在代码中使用方法的定义，请在映射中双击该方法，或将其选中并按**F12**，或右键单击它并选择 "**前往定义**"。

![在代码图上中转到方法的代码定义](../debugger/media/debuggermap_gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

若要将要跟踪的项添加到地图中，请右键单击方法，然后选择要跟踪的项。最近添加的项显示为绿色。

![与调用堆栈代码图上的方法相关的字段](../debugger/media/debuggermap_showedfields.png "DebuggerMap_ShowedFields")

>[!NOTE]
>默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 您可以通过选择代码图工具栏上的 "**包括父级**" 按钮，或者在添加项时按**Ctrl**来关闭和打开此功能。

![在调用堆栈代码图上的方法中显示字段](../debugger/media/debuggermap_showfields.png "DebuggerMap_ShowFields")

继续生成图以查看更多代码。

 ![请参见使用字段的方法：调用堆栈代码图](../debugger/media/debuggermap_findallreferences.png "DebuggerMap_FindAllReferences")

 ![在调用堆栈代码图上使用字段的方法](../debugger/media/debuggermap_foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="FindBugs"></a>使用映射查找 Bug
 通过代码可视化，可帮助你更快发现 Bug。 例如，假设要调查绘图应用中的 bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![向代码图添加另一个调用堆栈](../debugger/media/debuggermap_addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 不立即发挥作用的原因。

 修复 bug 并继续运行应用后，映射会将 `undo` 的新调用添加到 `Repaint`中：

 ![添加新的方法调用以调用堆栈上的代码图](../debugger/media/debuggermap_addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="share-the-map-with-others"></a>与他人共享地图

你可以导出映射，将其发送给使用 Microsoft Outlook 的其他用户，将其保存到你的解决方案，然后将其签入到版本控制中。

若要共享或保存地图，请使用代码图工具栏中的 "**共享**"。

![与其他人共享调用堆栈代码图](../debugger/media/debuggermap_sharewithothers.png "与他人共享调用堆栈代码图")

## <a name="see-also"></a>请参阅
[映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

[使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
