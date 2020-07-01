---
title: 创建调用堆栈的可视图 | Microsoft Docs
ms.date: 11/26/2018
ms.topic: how-to
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
ms.openlocfilehash: 2cf0cda942241ca77aa750624b6de25b5ae39391
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348530"
---
# <a name="create-a-visual-map-of-the-call-stack-while-debugging-c-visual-basic-c-javascript"></a>在调试时创建调用堆栈的可视图（C#、Visual Basic、C++ 和 JavaScript）

创建代码映射，以便在调试时对调用堆栈进行可视化跟踪。 可以在映射中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

若要查看演练，请观看此视频：[视频：通过代码图调试器集成进行可视化调试（第 9 频道）](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

若要详细了解使用代码图时能使用的命令和操作，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

>[!IMPORTANT]
>只能在 [Visual Studio Enterprise Edition](https://visualstudio.microsoft.com/downloads) 中创建代码图。

下面是代码图的简介：

 ![使用代码图上的调用堆栈调试](../debugger/media/debuggermap_overview.png "DebuggerMap_Overview")

## <a name="map-the-call-stack"></a><a name="MapStack"></a>映射调用堆栈

1. 在 Visual Studio Enterprise C#、Visual Basic 或者 JavaScript 项目中，若要开始调试，请选择“调试” > “开始调试”，或按 F5  。

1. 在应用进入中断模式或你单步执行某一函数之后，请选择“调试” > “代码图”，或按 Ctrl+Shift+`    。

   当前的调用堆栈在新代码图上显示为橙色：

   ![查看代码图上的调用堆栈](../debugger/media/debuggermap_seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

随着你继续调试，代码图会自动更新。 更改映射项或布局不会对代码造成任何影响。 你可随意在图上重命名、移动或移除任何内容。

若要获取有关某个项的详细信息，请将鼠标悬停至该项，然后查看其工具提示。 也可以选择工具栏中的“图例”来了解每个图标的含义。

![代码图图例](../debugger/media/debuggermap_showlegend.png "代码图图例")

>[!NOTE]
>代码图顶部如果出现消息“关系图可能基于旧版本的代码”，则说明在你上次更新图后，代码可能已发生更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

## <a name="map-external-code"></a>映射外部代码

默认情况下，只有你自己的代码会显示在图中。 若要查看图中的外部代码：

- 右键单击“调用堆栈”窗口，然后选择“显示外部代码” ：

  ![使用“调用堆栈”窗口显示外部代码](../debugger/media/debuggermap_callstackmenu.png "DebuggerMap_CallStackMenu")
- 或在 Visual Studio“工具”（或“调试”）>“选项” > “调试”中取消选择“启用‘仅我的代码’”    ：

  ![使用“选项”对话框显示外部代码](../debugger/media/debuggermap_debugoptions.png "DebuggerMap_DebugOptions")

## <a name="control-the-maps-layout"></a>控制代码图的布局

更改代码图的布局不会对代码造成任何影响。

若要控制图的布局，请选择代码图工具栏上的“布局”菜单。

在“布局”菜单中，可以进行以下操作：

- 更改默认布局。
- 若要停止自动重新排列代码图，请取消选择“调试时自动布局”。
- 若要在添加新项时尽可能少地重新排列代码图，请取消选择“增量布局”。

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a>对代码进行标注

可以添加注释以跟踪代码中的情况。

若要添加注释，请在代码图中右键单击，选择“编辑” > “新建注释”，然后键入注释内容 。

若要在注释中添加新行，请按 Shift+Enter 。

 ![向代码图上的调用堆栈添加注释](../debugger/media/debuggermap_addcomment.png "DebuggerMap_AddComment")

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a>使用下一个调用堆栈更新映射

在运行应用到下一个断点或单步执行函数时，代码图会自动添加新的调用堆栈。

![使用下一个调用堆栈更新代码图](../debugger/media/debuggermap_addclearcallstack.png "DebuggerMap_AddClearCallStack")

若要阻止代码图自动添加新的调用堆栈，请在代码图工具栏上选择“![在代码图上自动显示调用堆栈](../debugger/media/debuggermap_automaticupdateicon.gif "在代码图上自动显示调用堆栈")”。 代码图会继续突出显示现有的调用堆栈。 若要手动向图中添加当前的调用堆栈，请按 Ctrl+Shift+`  。

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a>向映射添加相关代码

现在你已获得一个采用 C# 或 Visual Basic 格式的代码图，可以添加字段、属性和其他方法等项，以跟踪代码中的情况。

若要转到代码中某个方法的定义，请在代码图中双击该方法，或将其选中并按 F12，或右键单击该方法并选择“转到定义” 。

![转到代码图上某方法的代码定义](../debugger/media/debuggermap_gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

若要将想跟踪的项添加到代码图中，请右键单击方法，然后选择想跟踪的项。最近添加的项显示为绿色。

![调用堆栈代码图上与某方法相关的字段](../debugger/media/debuggermap_showedfields.png "DebuggerMap_ShowedFields")

>[!NOTE]
>默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 通过选择代码图工具栏上的“包括父项”按钮或在添加项时按 Ctrl，可以关闭和开启此功能 。

![显示调用堆栈代码图上某方法中的字段](../debugger/media/debuggermap_showfields.png "DebuggerMap_ShowFields")

继续生成图以查看更多代码。

 ![查看使用字段的方法：调用堆栈代码图](../debugger/media/debuggermap_findallreferences.png "DebuggerMap_FindAllReferences")

 ![调用堆栈代码图上使用某字段的方法](../debugger/media/debuggermap_foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a>使用映射查找 Bug
 通过代码可视化，可帮助你更快发现 Bug。 例如，假设你正在调查某个绘图应用中的 Bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![向代码图添加另一个调用堆栈](../debugger/media/debuggermap_addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 不立即发挥作用的原因。

 在修复此 Bug 并继续运行应用后，图中增加了从 `undo` 到 `Repaint` 的新调用：

 ![向代码图上的调用堆栈添加新方法调用](../debugger/media/debuggermap_addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="share-the-map-with-others"></a>与他人共享此代码图

你可以导出代码图，然后通过 Microsoft Outlook 将其发送给其他人，或保存到你的解决方案中，再将其签入版本控制。

若要共享或保存代码图，请使用代码图工具栏中的“共享”。

![与他人共享调用堆栈代码图](../debugger/media/debuggermap_sharewithothers.png "与他人共享调用堆栈代码图")

## <a name="see-also"></a>请参阅
[映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

[使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

[使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
