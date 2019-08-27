---
title: 创建调用堆栈的直观映射 |Microsoft Docs
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
ms.openlocfilehash: 3de5a3f9e9c5b8f89a9c8917794247098ba12d06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62846549"
---
# <a name="create-a-visual-map-of-the-call-stack-while-debugging-c-visual-basic-c-javascript"></a>创建进行调试时的调用堆栈的直观映射 (C#，Visual Basic 中， C++，JavaScript)

创建代码映射，以便在调试时对调用堆栈进行可视化跟踪。 可以在映射中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

有关演练，请观看此视频：[视频：直观地调试与代码图调试器集成 (通道 9)](http://go.microsoft.com/fwlink/?LinkId=293418)

有关命令和操作可以使用代码图的详细信息，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

>[!IMPORTANT]
>您可以创建仅在代码图[Visual Studio Enterprise 版](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)。

下面是快速看一下代码映射：

 ![使用调用堆栈代码图上进行调试](../debugger/media/debuggermap_overview.png "DebuggerMap_Overview")

## <a name="MapStack"></a>映射调用堆栈

1. 在 Visual Studio Enterprise C#，Visual Basic 中， C++，或 JavaScript 项目中，通过选择启动调试**调试** > **启动调试**或按**F5**.

1. 你的应用进入中断模式或你单步执行函数后，选择**调试** > **代码图**，或按**Ctrl**+**Shift**+**`**.

   当前的调用堆栈在新代码图上显示为橙色：

   ![请参阅在代码图上的调用堆栈](../debugger/media/debuggermap_seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

在您继续进行调试的代码会自动映射更新。 更改地图项或布局不会影响任何方式中的代码。 你可随意在图上重命名、移动或移除任何内容。

若要获取有关某个项的详细信息，请悬停在其上方并查看项的工具提示。 您还可以选择**图例**在工具栏中，若要了解每个图标的含义。

![代码地图图例](../debugger/media/debuggermap_showlegend.png "代码地图图例")

>[!NOTE]
>消息**关系图可能基于代码的较旧版本**顶部的代码映射表示上次更新图后，代码可能已更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

## <a name="map-external-code"></a>映射外部代码

默认情况下，只有你自己的代码会显示在图中。 若要在地图上查看外部代码：

- 在中右击**调用堆栈**窗口，然后选择**显示外部代码**:

  ![显示外部代码中使用调用堆栈窗口](../debugger/media/debuggermap_callstackmenu.png "DebuggerMap_CallStackMenu")
- 或取消选中**启用 ' 仅我的代码**在 Visual Studio**工具**(或**调试**) >**选项** >  **调试**:

  ![显示外部代码使用选项对话框](../debugger/media/debuggermap_debugoptions.png "DebuggerMap_DebugOptions")

## <a name="control-the-maps-layout"></a>控制地图的布局

更改代码图的布局不会影响任何方式中的代码。

若要控制地图的布局，请选择**布局**图工具栏上的菜单。

在中**布局**菜单中，你可以：

- 更改默认布局。
- 停止通过取消选择自动重新排列图**调试时自动布局**。
- 添加项，通过取消选中时重新排列图尽可能少地**增量布局**。

## <a name="MakeNotes"></a>对代码进行标注

可以添加注释以跟踪代码中发生的情况。

若要添加注释，在代码图中右键单击并选择**编辑** > **新注释**，然后键入注释。

若要在注释中添加新行，请按**Shift**+**Enter**。

 ![添加注释代码图上的调用堆栈](../debugger/media/debuggermap_addcomment.png "DebuggerMap_AddComment")

## <a name="UpdateMap"></a>使用下一个调用堆栈更新映射

为运行您的应用程序到下一个断点或单步执行某一函数，地图会自动添加新的调用堆栈。

![使用下一个调用堆栈更新代码映射](../debugger/media/debuggermap_addclearcallstack.png "DebuggerMap_AddClearCallStack")

若要停止自动添加新的调用堆栈中的映射，请选择![显示调用自动堆栈代码图上](../debugger/media/debuggermap_automaticupdateicon.gif "显示调用自动堆栈代码图上")代码图工具栏上。 该映射将继续突出显示现有调用堆栈。 若要手动添加到映射的当前调用堆栈，请按**Ctrl**+**Shift**+**`**。

## <a name="AddRelatedCode"></a>向映射添加相关代码

现在，已在生成一个图中，C#或 Visual Basic 中，可以添加字段、 属性和其他方法，来跟踪代码中发生的情况等项目。

若要转到代码中方法的定义，双击方法在映射中，或选择它并按**F12**，或右键单击它，然后选择**转到定义**。

![转到代码图上的方法的代码定义](../debugger/media/debuggermap_gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

若要添加你想要跟踪对映射的项，请右键单击某个方法，并选择你想要跟踪的项。最近添加的项显示为绿色。

![调用堆栈代码图上的方法相关字段](../debugger/media/debuggermap_showedfields.png "DebuggerMap_ShowedFields")

>[!NOTE]
>默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 通过选择，禁用和启用此功能**包括父级**按钮在代码图工具栏上或按**Ctrl**时添加项。

![显示调用堆栈代码图上的方法中的字段](../debugger/media/debuggermap_showfields.png "DebuggerMap_ShowFields")

继续生成图以查看更多代码。

 ![请参阅使用字段的方法： 调用堆栈代码图](../debugger/media/debuggermap_findallreferences.png "DebuggerMap_FindAllReferences")

 ![在调用堆栈代码图使用的字段的方法](../debugger/media/debuggermap_foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="FindBugs"></a>使用映射查找 Bug
 通过代码可视化，可帮助你更快发现 Bug。 例如，假设正在调查的绘图应用程序中的 bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![将另一个调用堆栈添加到代码图](../debugger/media/debuggermap_addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 不立即发挥作用的原因。

 修复此 bug 并继续运行该应用程序后，此图将添加新的调用，从`undo`到`Repaint`:

 ![在代码图上添加新方法的调用堆栈](../debugger/media/debuggermap_addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="share-the-map-with-others"></a>与他人共享代码图

可以导出映射、 Microsoft outlook 向其他人发送它、 将其保存到您的解决方案，和签入版本控制。

若要共享或保存该映射，使用**共享**代码图工具栏中。

![与他人共享调用堆栈代码图](../debugger/media/debuggermap_sharewithothers.png "与他人共享调用堆栈代码图")

## <a name="see-also"></a>请参阅
[映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

[使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
