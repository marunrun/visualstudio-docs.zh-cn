---
title: 调试时映射调用堆栈上的方法
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- FSharp
- VB
- CSharp
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
caps.latest.revision: 43
author: MikeJo5000
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b55c677f4ba241260f1ebebc024a150dcd23eb19
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432172"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>在 Visual Studio 中调试时映射调用堆栈上的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建代码图，以便在调试时对调用堆栈进行可视化跟踪。 你可以在图中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

 ![使用调用堆栈代码图上进行调试](../debugger/media/debuggermap-overview.png "DebuggerMap_Overview")

 你将需要：

- [Visual Studio Enterprise](https://www.visualstudio.com/downloads/download-visual-studio-vs)

- 可调试的代码，例如 Visual C# .NET、Visual Basic .NET、C++、JavaScript 或 X++

  请参阅：[视频：使用代码图调试器集成 (通道 9) 直观地调试](http://go.microsoft.com/fwlink/?LinkId=293418)•[映射调用堆栈](#MapStack)•[记下的有关代码说明](#MakeNotes)•[更新映射与下一个调用堆栈](#UpdateMap)•[向地图添加相关的代码](#AddRelatedCode)•[使用图查找 bug](#FindBugs) •[问题与解答](#QA)

  有关命令和使用代码图时，可以使用的操作的详细信息，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

## <a name="MapStack"></a>映射调用堆栈

1. 开始调试。 （键盘：**F5**)

2. 你的应用进入中断模式或你单步执行函数后，请选择**Code Map**。 （键盘：**Ctrl** + **Shift** + **`**)

     ![选择代码图以开始映射调用堆栈](../debugger/media/debuggermap-choosecodemap.png "DebuggerMap_ChooseCodeMap")

     当前的调用堆栈在新代码图上显示为橙色：

     ![请参阅在代码图上的调用堆栈](../debugger/media/debuggermap-seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

     在你继续调试时，该代码图将自动更新。 请参阅[使用下一步的调用堆栈更新图](#UpdateMap)。

## <a name="MakeNotes"></a>对代码进行标注
 添加注释以跟踪代码发生的情况。 若要在注释中添加新行，请按**Shift + Return**。

 ![添加注释代码图上的调用堆栈](../debugger/media/debuggermap-addcomment.png "DebuggerMap_AddComment")

## <a name="UpdateMap"></a>使用下一个调用堆栈更新映射
 运行你的应用到下一个断点或单步执行某一函数。 此图将添加新的调用堆栈。

 ![使用下一个调用堆栈更新代码映射](../debugger/media/debuggermap-addclearcallstack.png "DebuggerMap_AddClearCallStack")

## <a name="AddRelatedCode"></a>向映射添加相关代码
 现在你已生成一个图，下一步做什么？ 如果你正在使用 Visual C# .NET 或 Visual Basic .NET，请添加诸如字段、属性和其他方法等项，以便跟踪代码发生的情况。

 双击某个方法以查看其代码定义，或者使用该方法的快捷菜单。 （键盘：选择方法在图上按**F12**)

 ![转到代码图上的方法的代码定义](../debugger/media/debuggermap-gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

 添加要在图上跟踪的项。

 ![显示调用堆栈代码图上的方法中的字段](../debugger/media/debuggermap-showfields.png "DebuggerMap_ShowFields")

> [!NOTE]
> 默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 尽管这很有用，您可以仅仅保留图通过关闭此功能使用**包括父级**图工具栏上或通过按按钮**CTRL**添加项时。

 ![调用堆栈代码图上的方法相关字段](../debugger/media/debuggermap-showedfields.png "DebuggerMap_ShowedFields")

 在这里，你可以轻松查看哪些方法使用了相同的字段。 最近添加的项显示为绿色。

 继续生成图以查看更多代码。

 ![请参阅使用字段的方法： 调用堆栈代码图](../debugger/media/debuggermap-findallreferences.png "DebuggerMap_FindAllReferences")

 ![在调用堆栈代码图使用的字段的方法](../debugger/media/debuggermap-foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="FindBugs"></a>使用映射查找 Bug
 通过代码可视化，可帮助你更快发现 Bug。 例如，假设你正在一个绘图程序中调查 Bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![将另一个调用堆栈添加到代码图](../debugger/media/debuggermap-addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 为何不立即发挥作用。

 在修复此 Bug 并继续运行程序后，图中增加了从 `undo` 到 `Repaint` 的新调用：

 ![在代码图上添加新方法的调用堆栈](../debugger/media/debuggermap-addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="QA"></a> 问题解答

- **并非所有调用将都显示在映射上。为什么?**

   默认情况下，只有你自己的代码会显示在图中。 若要查看外部代码，将其打开**调用堆栈**窗口：

   ![显示外部代码中使用调用堆栈窗口](../debugger/media/debuggermap-callstackmenu.png "DebuggerMap_CallStackMenu")

   或将其关闭**启用 ' 仅我的代码**在 Visual Studio 调试选项：

   ![显示外部代码使用选项对话框](../debugger/media/debuggermap-debugoptions.png "DebuggerMap_DebugOptions")

- **更改图是否会影响代码？**

   更改图不会对代码造成任何影响。 你可随意在图上重命名、移动或移除任何内容。

- **此消息是什么意思："关系图可能基于代码的较旧版本"？**

   在你上次更新图后，代码可能已发生更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

- **如何控制图的布局？**

   打开**布局**图工具栏上的菜单：

  - 更改默认布局。

  - 若要停止自动重新排列图，关闭**调试时自动布局**。

  - 若要添加项时，重新排列图降至最低，请关闭**增量布局**。

- **可以与他人共享代码图？**

   你可以导出映射，将其发送给他人（如果你有 Microsoft Outlook）或保存到你的解决方案中，以便你将其签入 Team Foundation 版本控制。

   ![与他人共享调用堆栈代码图](../debugger/media/debuggermap-sharewithothers.png "DebuggerMap_ShareWithOthers")

- **如何停止自动添加新的调用堆栈中的映射？**

   选择![按钮&#45;显示调用自动堆栈代码图上](../debugger/media/debuggermap-automaticupdateicon.gif "DebuggerMap_AutomaticUpdateIcon")图工具栏上。 若要手动添加到映射的当前调用堆栈，请按**Ctrl** + **Shift** + **`**。

   在你进行调试时，图中将继续突出显示现有调用堆栈。

- **项图标和箭头代表什么？**

   若要获取有关某个项的详细信息，请将鼠标指针移动到它上方，然后查看该项的工具提示。 此外可以查看**图例**若要了解每个图标的含义。

   ![调用堆栈代码图上的图标是什么意思？](../debugger/media/debuggermap-showlegend.png "DebuggerMap_ShowLegend")

  请参阅：[映射调用堆栈](#MapStack)•[记下的有关代码说明](#MakeNotes)•[使用下一步的调用堆栈更新图](#UpdateMap)•[向地图添加相关的代码](#AddRelatedCode)•[查找 bug使用映射](#FindBugs)

## <a name="see-also"></a>请参阅
 [映射解决方案之间的依赖项](../modeling/map-dependencies-across-your-solutions.md)[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)[发现潜在的问题，使用代码映射分析器](../modeling/find-potential-problems-using-code-map-analyzers.md)[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
