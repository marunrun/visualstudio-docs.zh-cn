---
title: 使用 IntelliTrace 查看上一应用状态
description: 了解如何拍摄快照和使用 IntelliTrace 单步后退查看快照
ms.custom: seodec18
ms.date: 09/19/2018
ms.topic: tutorial
ms.assetid: 7c60d929-d993-49dc-9db3-43b30be9912b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83d444cb5e3345d79ca6e1422982c0ecd37e4287
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825524"
---
# <a name="inspect-previous-app-states-using-intellitrace-step-back-in-visual-studio-visual-studio-enterprise"></a>在 Visual Studio (Visual Studio Enterprise) 中，使用 IntelliTrace 单步后退来检查旧应用状态

IntelliTrace 后退会在每个断点处及调试器步骤事件发生时自动拍摄应用程序的快照。 凭借记录的快照便可以返回到上一个断点或步骤，并查看当时应用程序的状态。 如果希望查看以前的应用程序状态，但不想重新启动调试或重新创建所需应用状态，使用 IntelliTrace 后退可以节省时间。

自 Visual Studio Enterprise 2017 版本 15.5 及更高版本起提供 IntelliTrace 后退功能，并且它需要 Windows 10 周年更新或更高版本。 当前支持将该功能用于调试 ASP.NET、WinForms、WPF、托管控制台应用和托管类库。 从 Visual Studio 2017 Enterprise 版本 15.7 开始，ASP.NET Core 和.NET Core 也支持该功能。 从 Visual Studio 2017 Enterprise 版本 15.9 预览版 2 开始，面向 Windows 的本机应用也支持该功能。 当前不支持调试 UWP 应用程序。

在本教程中，你将：

> [!div class="checklist"]
> * 启用 IntelliTrace 事件和快照
> * 使用后退和前进命令导航事件
> * 查看事件快照

## <a name="enable-intellitrace-events-and-snapshots-mode"></a>启用 IntelliTrace 事件和快照模式

1. 在 Visual Studio Enterprise 中打开项目。

1. 打开“工具” > “选项” > “IntelliTrace”设置，并选择“IntelliTrace事件和快照”选项     。

    从 Visual Studio 2017 Enterprise 版本 15.9 预览版 2 开始，本选项为“IntelliTrace 快照(托管和本机)”  。

    ![启用 IntelliTrace 事件和快照模式](../debugger/media/intellitrace-enable-snapshots.png "启用 IntelliTrace 事件和快照模式")

1. 如果想要配置用于查看异常发生时的快照的选项，请从“选项”对话框选择“IntelliTrace” > “高级”    。

    这些选项从 Visual Studio 2017 Enterprise 版本 15.7 开始提供。

    ![配置异常发生时快照的行为](../debugger/media/intellitrace-enable-snapshots-on-exceptions.png)

    启用事件和快照时，也默认启用异常发生时拍摄快照。 可以取消选中“在异常事件发生时收集快照”来禁用异常发生时拍摄快照  。 启用此功能后，可拍摄未处理异常的快照。 对于已处理的异常，只有在引发异常时且该异常不属于之前引发的异常的再次引发时才会拍摄快照。 从下拉列表中选择一个值，可以设置异常发生时拍摄的最大快照数。 每次应用进入中断模式时该最大值都适用（例如应用命中断点时）。

    > [!NOTE]
    > 仅为 IntelliTrace 记录的异常事件拍摄快照。 对于托管代码，选择“工具” > “选项” > “IntelliTrace 事件”，可以指定 IntelliTrace 记录的事件    。

1. 在项目中设置一个或多个断点并开始调试（按 F5），或通过逐步执行代码来启动调试（F10 或 F11）    。

    IntelliTrace 在每个调试器步骤、断点事件和未处理异常事件发生时拍摄应用程序进程的快照。 这些事件和其他 IntelliTrace 事件一起记录在“诊断工具”窗口中的“事件”选项卡上   。 若要打开此窗口，请选择“调试” > “Windows” > “显示诊断工具”    。

    快照功能可用的事件旁边会显示照相机图标。

    ![带有快照的“事件”选项卡](../debugger/media/intellitrace-events-tab-with-snapshots.png "带有断点处和步骤执行时拍摄的快照的“事件”选项卡")

    由于性能原因，单步执行过快时不拍摄快照。 如果该步骤旁没有显示照相机图标，请尝试将单步执行速度放慢。

## <a name="navigate-and-view-snapshots"></a>导航和查看快照

1. 使用“调试”工具栏中的“后退”(Alt + [) 和“前进”(Alt + ]) 按钮，在事件间进行导航   。

    这些按钮用于浏览“诊断工具”窗口中“事件”选项卡上显示的事件   。 后退或前进到某个事件会自动激活所选事件的[历史调试](../debugger/historical-debugging.md)。

    ![“后退”和“前进”按钮](../debugger/media/intellitrace-step-back-icons-description.png "Step Backward and Step Forward buttons")

    后退或前进时，Visual Studio 进入历史调试模式。 在此模式下，调试器上下文将切换到记录所选事件时的时间。 Visual Studio 还将指针移动到源窗口中的相应代码行。

    在此视图中，可以检查“调用堆栈”、“局部变量”、“自动”以及“监视”窗口中的值     。 还可以在变量上悬停鼠标，以在“即时”窗口上查看数据提示并进行表达式求值  。 看到的数据源于在该时间点拍摄的应用程序进程的快照。

    因此，举例来说，如果命中断点并执行步骤 (F10)，则“后退”按钮将在断点对应的代码行上将 Visual Studio 置于历史模式   。

    ![在带有快照的事件上激活历史模式](../debugger/media/intellitrace-historical-mode-with-snapshot.png "在带有快照的事件上激活历史模式")

2. 若要返回到实时执行，请在信息栏中选择“继续”(F5) 或单击“返回实时调试”链接   。

3. 还可以从“事件”选项卡查看快照  。若要执行此操作，请选择带有快照的事件，然后单击“激活历史调试”  。

    ![事件上的“激活历史调试”](../debugger/media/intellitrace-activate-historical-debugging.png "Activate Historical Debugging on an event")

    与“设置下一语句”命令不同，查看快照不会重新运行代码；它提供在过去发生的某个时间点的应用程序状态的静态视图  。

    ![IntelliTrace 后退的概述](../debugger/media/intellitrace-step-back-overview.png "Overview of IntelliTrace Step-back")

    若要了解有关如何在 Visual Studio 中检查变量的详细信息，请参阅[初探调试器](../debugger/debugger-feature-tour.md)

## <a name="frequently-asked-questions"></a>常见问题

#### <a name="how-is-intellitrace-step-back-different-from-intellitrace-events-only-mode"></a>IntelliTrace 后退功能与 IntelliTrace 仅事件模式有何不同？

仅事件模式下的 IntelliTrace 允许在调试器步骤发生时和断点处激活历史调试。 但是，IntelliTrace 只捕获已打开的“局部变量”和“自动”窗口中的数据，并且只捕获已展开的且在视图中的数据   。 在仅事件模式下，通常没有变量和复杂对象的完整视图。 此外，不支持在“监视”窗口中进行表达式求值和查看数据  。

在事件和快照模式下，IntelliTrace 捕获应用程序进程（包括复杂对象）的全部快照。 在代码行上，可以看到如同在断点处停止时看到的信息（且之前是否已展开信息并不重要）。 查看快照时，还支持表达式求值。  

#### <a name="what-is-the-performance-impact-of-this-feature"></a>此功能对性能有何影响？ 

对总体单步执行性能的影响取决于应用程序。 拍摄快照大约耗用 30 毫秒。 拍摄快照时，为应用的进程创建分支且分支副本会挂起。 查看快照时，Visual Studio 将附加到进程的分支副本。 对于每个快照，Visual Studio 仅复制页表并将页设置为写入时复制。 如果堆上的对象在具有关联快照的调试器步骤之间更改，则将复制相应的页表，而产生最小的内存成本。 如果 Visual Studio 检测到拍摄快照内存不足，则不会拍摄。

## <a name="known-issues"></a>已知问题
* 如果在低于 Windows 10 Fall Creators Update (RS3) 的 Windows 版本上使用 IntelliTrace 事件和快照模式且应用程序的调试平台目标为 x86，则 IntelliTrace 不会拍摄快照。

    解决方法：
  * 如果使用的是 Windows 10 周年更新 (RS1) 和低于 10.0.14393.2273 的版本，请[安装 KB4103720](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)。
  * 如果使用的是 Windows 10 Creators Update (RS2) 和低于 10.0.15063.1112 的版本，请[安装 KB4103722](https://support.microsoft.com/help/4103722/windows-10-update-4103722)。
  * 安装或升级到 Windows 10 Creators Update (RS3)。
  * 或者：
    1. 用 Visual Studio 安装程序安装用于桌面的 VC++ 2015.3 v140 工具集组件 (x86, x64)。
    2. 生成目标应用程序。
    3. 在命令行中，使用 editbin 工具为目标可执行文件设置 `Largeaddressaware` 标志。 例如，可能会使用此命令（更新路径后）："C:\Program Files (x86)\Microsoft Visual Studio\Preview\Enterprise\VC\Tools\MSVC\14.12.25718\bin\Hostx86\x86\editbin.exe" /Largeaddressaware "C:\Path\To\Application\app.exe"。
    4. 若要启用调试，请按 F5  。 现在，在调试器步骤执行时和断点处拍摄快照。

       > [!Note]
       > 每次使用更改重新生成可执行文件时，必须设置 `Largeaddressaware` 标志。

* 在使用永久内存映射文件的应用程序上拍摄应用程序进程的快照时，带有快照的进程在内存映射文件上保有排他锁（即使父级进程已释放其锁）。 其他进程仍然能够读取（但不能写入）内存映射文件。

  解决方法：
  * 结束调试会话，以清除所有快照。

* 调试其进程中有大量唯一内存区域的应用程序（例如加载大量 DLL 的应用程序）时，带有快照的单步执行性能可能受影响。 以后的 Windows 版本将解决这个问题。 如果正遭遇此问题，请在 stepback@microsoft.com 上联系我们。

* 在事件和快照模式下使用“调试”>“IntelliTrace”>“保存 IntelliTrace 会话”来保存文件时，在 .itrace 文件中无法使用快照捕获的其他数据  。 在断点处和单步执行事件时，将看到如同在 IntelliTrace 仅事件模式下保存文件时看到的信息。

## <a name="next-steps"></a>后续步骤

在本教程中，已经了解了如何使用 IntelliTrace 后退。 你可能想要了解有关其他 IntelliTrace 功能的详细信息。

> [!div class="nextstepaction"]
> [IntelliTrace 功能](../debugger/intellitrace-features.md)
