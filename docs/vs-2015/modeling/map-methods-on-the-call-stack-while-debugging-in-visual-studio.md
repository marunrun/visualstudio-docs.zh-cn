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
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2a2c6e95822794394dbdfc7f53104b31b7c17ea9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296071"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>在 Visual Studio 中调试时映射调用堆栈上的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建代码图，以便在调试时对调用堆栈进行可视化跟踪。 你可以在图中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

 ![Debugging with call stacks on code maps](../debugger/media/debuggermap-overview.png "DebuggerMap_Overview")

 你将需要：

- [Visual Studio Enterprise](https://www.visualstudio.com/downloads/download-visual-studio-vs)

- 可调试的代码，例如 Visual C# .NET、Visual Basic .NET、C++、JavaScript 或 X++

  See: [Video: Debug visually with Code Map debugger integration (Channel 9)](https://go.microsoft.com/fwlink/?LinkId=293418) • [Map the call stack](#MapStack) • [Make notes about the code](#MakeNotes) • [Update the map with the next call stack](#UpdateMap) • [Add related code to the map](#AddRelatedCode) • [Find bugs using the map](#FindBugs) • [Q & A](#QA)

  For details of the commands and actions you can use when working with code maps, see [Browse and rearrange code maps](../modeling/browse-and-rearrange-code-maps.md).

## <a name="MapStack"></a>映射调用堆栈

1. 开始调试。 (Keyboard: **F5**)

2. After your app enters break mode or you step into a function, choose **Code Map**. (Keyboard: **Ctrl** + **Shift** +  **`** )

     ![Choose Code Map to start mapping call stack](../debugger/media/debuggermap-choosecodemap.png "DebuggerMap_ChooseCodeMap")

     当前的调用堆栈在新代码图上显示为橙色：

     ![See call stack on code map](../debugger/media/debuggermap-seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

     在你继续调试时，该代码图将自动更新。 See [Update the map with the next call stack](#UpdateMap).

## <a name="MakeNotes"></a>对代码进行标注
 添加注释以跟踪代码发生的情况。 To add a new line in a comment, press **Shift + Return**.

 ![Add comment to call stack on code map](../debugger/media/debuggermap-addcomment.png "DebuggerMap_AddComment")

## <a name="UpdateMap"></a>使用下一个调用堆栈更新映射
 运行你的应用到下一个断点或单步执行某一函数。 此图将添加新的调用堆栈。

 ![Update code map with next call stack](../debugger/media/debuggermap-addclearcallstack.png "DebuggerMap_AddClearCallStack")

## <a name="AddRelatedCode"></a>向映射添加相关代码
 现在你已生成一个图，下一步做什么？ 如果你正在使用 Visual C# .NET 或 Visual Basic .NET，请添加诸如字段、属性和其他方法等项，以便跟踪代码发生的情况。

 双击某个方法以查看其代码定义，或者使用该方法的快捷菜单。 (Keyboard: Select the method on the map and press **F12**)

 ![Go to code definition for a method on code map](../debugger/media/debuggermap-gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

 添加要在图上跟踪的项。

 ![Show fields in a method on call stack code map](../debugger/media/debuggermap-showfields.png "DebuggerMap_ShowFields")

> [!NOTE]
> 默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 While this is useful, you can keep the map simple by turning off this feature using the **Include Parents** button on the map toolbar, or by pressing **CTRL** when you add items.

 ![Fields related to a method on call stack code map](../debugger/media/debuggermap-showedfields.png "DebuggerMap_ShowedFields")

 在这里，你可以轻松查看哪些方法使用了相同的字段。 最近添加的项显示为绿色。

 继续生成图以查看更多代码。

 ![See methods that use a field: call stack code map](../debugger/media/debuggermap-findallreferences.png "DebuggerMap_FindAllReferences")

 ![Methods that use a field on call stack code map](../debugger/media/debuggermap-foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="FindBugs"></a>使用映射查找 Bug
 通过代码可视化，可帮助你更快发现 Bug。 例如，假设你正在一个绘图程序中调查 Bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![Add another call stack to code map](../debugger/media/debuggermap-addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 为何不立即发挥作用。

 在修复此 Bug 并继续运行程序后，图中增加了从 `undo` 到 `Repaint` 的新调用：

 ![Add new method call to call stack on code map](../debugger/media/debuggermap-addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="QA"></a> 问题解答

- **Not all calls appear on the map. Why?**

   默认情况下，只有你自己的代码会显示在图中。 To see external code, turn it on in the **Call Stack** window:

   ![Display external code using the Call Stack window](../debugger/media/debuggermap-callstackmenu.png "DebuggerMap_CallStackMenu")

   or turn off **Enable Just My Code** in the Visual Studio debugging options:

   ![Show external code using Options dialog](../debugger/media/debuggermap-debugoptions.png "DebuggerMap_DebugOptions")

- **Does changing the map affect the code?**

   更改图不会对代码造成任何影响。 你可随意在图上重命名、移动或移除任何内容。

- **What does this message mean: “The diagram may be based on an older version of the code”?**

   在你上次更新图后，代码可能已发生更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

- **How do I control the map’s layout?**

   Open the **Layout** menu on the map toolbar:

  - 更改默认布局。

  - To stop rearranging the map automatically, turn off **Automatically Layout when Debugging**.

  - To rearrange the map as little as possible when you add items, turn off **Incremental Layout**.

- **Can I share the map with others?**

   你可以导出映射，将其发送给他人（如果你有 Microsoft Outlook）或保存到你的解决方案中，以便你将其签入 Team Foundation 版本控制。

   ![Share call stack code map with others](../debugger/media/debuggermap-sharewithothers.png "DebuggerMap_ShareWithOthers")

- **How do I stop the map from adding new call stacks automatically?**

   Choose ![Button &#45; Show call stack on code map automatically](../debugger/media/debuggermap-automaticupdateicon.gif "DebuggerMap_AutomaticUpdateIcon") on the map toolbar. To manually add the current call stack to the map, press **Ctrl** + **Shift** +  **`** .

   在你进行调试时，图中将继续突出显示现有调用堆栈。

- **What do the item icons and arrows mean?**

   若要获取有关某个项的详细信息，请将鼠标指针移动到它上方，然后查看该项的工具提示。 You can also look at the **Legend** to learn what each icon means.

   ![What do icons on the call stack code map mean?](../debugger/media/debuggermap-showlegend.png "DebuggerMap_ShowLegend")

  See: [Map the call stack](#MapStack) • [Make notes about the code](#MakeNotes) • [Update the map with the next call stack](#UpdateMap) • [Add related code to the map](#AddRelatedCode) • [Find bugs using the map](#FindBugs)

## <a name="see-also"></a>请参阅
 [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md) [Use code maps to debug your applications](../modeling/use-code-maps-to-debug-your-applications.md) [Find potential problems using code map analyzers](../modeling/find-potential-problems-using-code-map-analyzers.md) [Browse and rearrange code maps](../modeling/browse-and-rearrange-code-maps.md)
