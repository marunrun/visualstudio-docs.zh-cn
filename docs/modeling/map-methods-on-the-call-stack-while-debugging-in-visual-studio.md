---
title: 调试时映射调用堆栈上的方法
ms.date: 11/04/2016
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8641a677ae36ad5a3c1f0f4344fc5c12b8798d7d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445137"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>在 Visual Studio 中调试时映射调用堆栈上的方法

创建代码映射，以便在调试时对调用堆栈进行可视化跟踪。 你可以在图中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

 ![使用代码图上的调用堆栈调试](../debugger/media/debuggermap_overview.png)

 你将需要：

 ::: moniker range="vs-2017"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)

::: moniker-end

- 可以调试，如 Visual C#、 Visual Basic、 c + +、 JavaScript 或 X + + 的代码

  请参阅：

- [视频：直观地调试与代码图调试器集成 (通道 9)](http://go.microsoft.com/fwlink/?LinkId=293418)

- [映射调用堆栈](#MapStack)

- [记下的有关代码说明](#MakeNotes)

- [使用下一个调用堆栈更新图](#UpdateMap)

- [向映射添加相关的代码](#AddRelatedCode)

- [查找使用映射的 bug](#FindBugs)

- [问题与解答](#QA)

  有关命令和使用代码图时，可以使用的操作的详细信息，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

## <a name="MapStack"></a>映射调用堆栈

1. 开始调试。 （键盘：**F5**)

2. 你的应用进入中断模式或你单步执行函数后，请选择**Code Map**。 （键盘：**Ctrl** + **Shift** + **`**)

     ![选择代码图以开始映射调用堆栈](../debugger/media/debuggermap_choosecodemap.png)

     当前的调用堆栈在新代码图上显示为橙色：

     ![查看代码图上的调用堆栈](../debugger/media/debuggermap_seeundocallstack.png)

     在你继续调试时，该代码图将自动更新。 请参阅[使用下一步的调用堆栈更新图](#UpdateMap)。

## <a name="MakeNotes"></a>对代码进行标注

 添加注释以跟踪代码中发生的情况。 若要在注释中添加新行，请按**Shift + Return**。

 ![向代码图上的调用堆栈添加注释](../debugger/media/debuggermap_addcomment.png)

## <a name="UpdateMap"></a>使用下一个调用堆栈更新映射

 运行你的应用到下一个断点或单步执行某一函数。 此图将添加新的调用堆栈。

 ![使用下一个调用堆栈更新代码图](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="AddRelatedCode"></a>向映射添加相关代码

 现在你已生成图-什么下一步？ 如果您正在使用 C# 或 Visual Basic，添加项，例如字段、 属性和其他方法，来跟踪代码中发生的情况。

 双击某个方法以查看其代码定义，或者使用该方法的快捷菜单。 （键盘：选择方法在图上按**F12**)

 ![转到代码图上某方法的代码定义](../debugger/media/debuggermap_gotocodedefinition.png)

 添加要在图上跟踪的项。

 ![显示调用堆栈代码图上某方法中的字段](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> 默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 尽管这很有用，您可以仅仅保留图通过关闭此功能使用**包括父级**图工具栏上或通过按按钮**CTRL**添加项时。

 ![调用堆栈代码图上与某方法相关的字段](../debugger/media/debuggermap_showedfields.png)

 在这里，你可以轻松查看哪些方法使用了相同的字段。 最近添加的项显示为绿色。

 继续生成图以查看更多代码。

 ![查看使用字段的方法：调用堆栈代码图](../debugger/media/debuggermap_findallreferences.png)

 ![调用堆栈代码图上使用某字段的方法](../debugger/media/debuggermap_foundallreferences.png)

## <a name="FindBugs"></a>使用映射查找 Bug

 通过代码可视化，可帮助你更快发现 Bug。 例如，假设要研究一个绘图程序中的 bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![向代码图添加另一个调用堆栈](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 不立即发挥作用的原因。

 在修复此 Bug 并继续运行程序后，图中增加了从 `undo` 到 `Repaint` 的新调用：

 ![向代码图上的调用堆栈添加新方法调用](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="QA"></a> 问题解答

- **并非所有调用将都显示在映射上。为什么?**

   默认情况下，只有你自己的代码会显示在图中。 若要查看外部代码，将其打开**调用堆栈**窗口：

   ![使用“调用堆栈”窗口显示外部代码](../debugger/media/debuggermap_callstackmenu.png)

   或将其关闭**启用 ' 仅我的代码**在 Visual Studio 调试选项：

   ![使用“选项”对话框显示外部代码](../debugger/media/debuggermap_debugoptions.png)

- **更改图是否会影响代码？**

   更改图不会影响任何方式中的代码。 你可随意在图上重命名、移动或移除任何内容。

- **此消息是什么意思："关系图可能基于代码的较旧版本"？**

   在你上次更新图后，代码可能已发生更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

- **如何控制图的布局？**

   打开**布局**图工具栏上的菜单：

  - 更改默认布局。

  - 若要停止自动重新排列图，关闭**调试时自动布局**。

  - 若要添加项时，重新排列图降至最低，请关闭**增量布局**。

- **可以与他人共享代码图？**

   可以导出该映射，将其发送给其他人，如果你有 Microsoft Outlook，或将其保存到你的解决方案，因此您可以将其签入源代码管理。

   ![与他人共享调用堆栈代码图](../debugger/media/debuggermap_sharewithothers.png)

- **如何停止自动添加新的调用堆栈中的映射？**

   选择![按钮&#45;显示调用自动堆栈代码图上](../debugger/media/debuggermap_automaticupdateicon.gif)图工具栏上。 若要手动添加到映射的当前调用堆栈，请按**Ctrl** + **Shift** + **`**。

   图中将继续进行调试时突出显示地图上的现有调用堆栈。

- **项图标和箭头代表什么？**

   若要获取有关某个项的详细信息，请将鼠标指针移动它并查看项的工具提示。 此外可以查看**图例**若要了解每个图标的含义。

   ![调用堆栈代码图上各图标的含义](../debugger/media/debuggermap_showlegend.png)

  请参阅：

- [映射调用堆栈](#MapStack)

- [记下的有关代码说明](#MakeNotes)

- [使用下一个调用堆栈更新图](#UpdateMap)

- [向映射添加相关的代码](#AddRelatedCode)

- [查找使用映射的 bug](#FindBugs)

## <a name="see-also"></a>请参阅

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
