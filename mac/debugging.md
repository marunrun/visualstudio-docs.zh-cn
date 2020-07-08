---
title: 使用 Visual Studio for Mac 调试
description: 调试是编程中常见且必要的部分。 Visual Studio for Mac 作为成熟的 IDE，具有一整套方便调试的功能。 本文将介绍如何在 Visual Studio for Mac 中充分使用调试功能，包括从安全调试到数据可视化效果。
author: therealjohn
ms.author: johmil
ms.date: 5/13/2020
ms.technology: vs-ide-debug
ms.assetid: BB7A084D-9AC2-48B5-8076-6C8518796BBA
ms.topic: overview
ms.openlocfilehash: 09a761a8269fa40c3fab49a34b3e43a7f0ec63cd
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939072"
---
# <a name="debugging-with-visual-studio-for-mac"></a>使用 Visual Studio for Mac 调试

Visual Studio for Mac 提供支持 .Net Core、.NET Framework、Unity 和 Xamarin 应用程序的调试器。

Visual Studio for Mac 使用 [Mono 软调试器](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)，该调试器在 Mono 运行时中实施，以便 Visual Studio for Mac 跨所有平台调试托管代码。

## <a name="the-debugger"></a>调试器

Visual Studio for Mac 使用 Mono 软调试器来调试所有 Xamarin 应用程序中的托管（C# 或 F#）代码。 Mono 软调试器不同于常规调试器，因为它是内置于 Mono 运行时的协作式调试器；生成的代码和 Mono 运行时与 IDE 协作提供调试体验。 Mono 运行时通过网络协议公开调试功能，可以阅读 [Mono 文档](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger-wire-format/)，了解详细信息。

硬调试器（如 [LLDB]( http://lldb.llvm.org/index.html) 或 [GDB]( https://www.gnu.org/software/gdb/)）在不了解受调试的程序或不与其协作的情况下控制程序，但如果需要调试本机 iOS 或 Android 代码，则该调试器对于调试 Xamarin 应用程序仍十分有用。

对于 .NET Core 和 ASP.NET Core 应用程序，Visual Studio for Mac 使用 .NET Core 调试器。 此调试器也是协作式调试器，适用于 .NET 运行时。

## <a name="using-the-debugger"></a>使用调试器

若要开始调试应用程序，请始终确保将配置设置为“调试”。 调试配置提供一组实用工具来支持调试，如断点、使用数据可视化工具和查看调用堆栈：

![调试配置](media/debugging-image_0.png)

## <a name="setting-a-breakpoint"></a>设置断点

若要在 IDE 中设置断点，请在想要中断的代码行号旁边，单击编辑器的空白区：

![在边距中设置断点](media/debugging-image0.png)

可通过转到“断点”面板查看代码中已设置的所有断点：

![断点列表](media/debugging-image0a.png)

## <a name="start-debugging"></a>“启动调试”

若要开始调试，请选择目标浏览器、设备或模拟器/仿真器：

![调试配置](media/debugging-image_0.png)
![选择目标设备](media/debugging-image1.png)

然后通过按“播放”按钮或“Cmd + 返回”部署应用程序 。 命中断点时，代码会以黄色突出显示：

![突出显示表明已命中断点](media/debugging-image2.png)

此时，可使用调试工具（如用于检查对象的值的工具）获取代码中所发生情况的相关详细信息：

![调试可视化效果](media/debugging-image3.png)

## <a name="conditional-breakpoints"></a>条件断点

还可以设置规则，规定应该发生断点的情况，这称为添加“条件断点”。 若要设置条件断点，请访问“断点属性”窗口。具体有以下两种操作方法：

* 若要添加新的条件断点，请右键单击编辑器边缘（即要设置断点的代码行号左侧），再选择“新建断点”：

 ![断点上下文菜单](media/debugging-image4.png)

* 若要向现有断点添加条件，请右键单击该断点并选择“断点属性”，或如下图所示在“断点”面板中选择“编辑断点”按钮： 

 ![在“断点”面板中编辑现有断点](media/debugging-image5.png)

然后可输入想要断点发生的条件：

 ![编辑断点条件](media/debugging-image6.png)

## <a name="stepping-through-code"></a>逐句通过代码

到达断点时，调试工具使用户能够控制该程序的执行。 Visual Studio for Mac 将显示四个按钮，使用户能够逐行运行代码。 在 Visual Studio for Mac 中，它们如下所示：

 ![用于逐行执行代码的按钮](media/debugging-image7.png)

以下是四个按钮：

* 播放 - 此按钮开始执行代码，直至下一个断点处。
* 单步跳过 - 此按钮执行下一行代码。 如果下一行是函数调用，“单步跳过”将执行该函数，并在该函数后的下一行代码停止。
* 单步执行 - 此按钮也执行下一行代码。 如果下一行是函数调用，“单步执行”将在该函数的第一行停止，允许继续进行函数的逐行调试。 如果下一行不是函数，其行为与“单步跳过”相同。
* 跳出 - 此按钮返回到调用当前函数的代码行。

## <a name="change-which-statement-is-executed-next"></a>更改要执行的下一条语句

调试器暂停时，边距中的箭头会显示下一条要执行的代码行。 可以单击箭头并将其拖至不同的代码行，以更改将执行的语句。 还可以通过右键单击代码行，然后从上下文菜单中选择“设置下一条语句”来实现同一操作。

![拖放箭头以设置下一条语句](media/debugger-drag-setnextstatement.gif)

> [!CAUTION]
> 更改当前执行行可能会导致应用程序中出现意外行为。 在某些情况下，无法更改要执行的下一条语句。 例如，无法将箭头从一个方法拖动到另一个方法。 在这些不受支持的情况下，Visual Studio for Mac 将显示一个对话框，告知你无法更改当前执行行。 

## <a name="debugging-monos-class-libraries"></a>调试 Mono 类库

Xamarin 产品随附用于 Mono 类库的源代码，可使用此代码在调试器中单步执行，查看内部工作原理。

由于此功能在调试过程中会占用更多内存，因此默认禁用。

若要启用此功能，请浏览到“Visual Studio for Mac”>“首选项”>“调试器”，并确保“单步执行外部代码”为“选中”状态，如下所示：

![“单步执行外部代码”选项](media/debugging-image8.png)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试 (Windows)](/visualstudio/debugger/)
