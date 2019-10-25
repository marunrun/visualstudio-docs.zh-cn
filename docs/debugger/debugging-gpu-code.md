---
title: 调试 GPU 代码 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: c7e77a5a-cb57-4b11-9187-ecc89acc8775
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db053317b3678cfaa7ee0ed6061074b156359d2f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738213"
---
# <a name="debugging-gpu-code"></a>调试 GPU 代码
可以调试在图形处理单元 (GPU) 上运行的 C++ 代码。 Visual Studio 中的 GPU 调试支持包括争用检测、启动进程并附加到进程以及与调试窗口集成。

## <a name="supported-platforms"></a>支持的平台
 [!INCLUDE[win7](../debugger/includes/win7_md.md)]、[!INCLUDE[win8](../debugger/includes/win8_md.md)]、[!INCLUDE[winsvr08_r2](../debugger/includes/winsvr08_r2_md.md)] 和 [!INCLUDE[winserver8](../debugger/includes/winserver8_md.md)] 上支持调试。 对于在软件模拟器上进行的调试，需要 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或 [!INCLUDE[winserver8](../debugger/includes/winserver8_md.md)]。 对于在硬件上进行的调试，您必须为图形卡安装驱动程序。 并非所有硬件供应商都实现所有调试器功能。 有关限制，请参阅供应商文档。

> [!NOTE]
> 希望在 Visual Studio 中支持 GPU 调试的独立硬件供应商必须创建一个 DLL, 该 DLL 实现 VSD3DDebug 接口并面向其自己的驱动程序。

## <a name="configuring-gpu-debugging"></a>配置 GPU 调试
 调试器无法同时在同一应用执行中的 CPU 代码和 GPU 代码处中断。 默认情况下，调试器在 CPU 代码处中断。 若要调试 GPU 代码，请使用以下两个步骤之一：

- 在“标准”工具栏上的“调试类型”列表中，选择“仅 GPU”。

- 在“解决方案资源管理器”中，在项目的快捷菜单上，选择“属性”。 在“属性页”对话框中，选择“调试”，然后在“调试器类型”列表中选择“仅 GPU”。

## <a name="launching-and-attaching-to-applications"></a>启动并附加到应用程序
 可以使用 Visual Studio 调试命令来启动和停止 GPU 调试。 有关详细信息，请参阅[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。 还可以将 GPU 调试器附加到正在运行的进程，但仅在该进程执行 GPU 代码时才能这样做。 有关详细信息，请参阅[附加到运行中的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

## <a name="run-current-tile-to-cursor-and-run-to-cursor"></a>“将当前 Tile 运行到光标处”和“运行到光标处”
 在 GPU 上进行调试时，可以通过两个选项运行到光标位置。 代码编辑器的快捷菜单上提供了这两个选项的命令。

1. “运行到光标处”命令可运行应用程序，直到其达到光标位置，然后中断。 这并不表示当前线程运行到光标处；相反，这意味着第一个到达光标点的线程会触发中断。 请参阅[使用调试器在代码中导航](../debugger/navigating-through-code-with-the-debugger.md)

2. “将当前 Tile 运行到光标处”命令可运行应用程序，直到当前 Tile 中的所有线程到达光标处，然后中断。

## <a name="debugging-windows"></a>“调试”窗口
 通过使用某些调试窗口，您可以检查、标记和冻结 GPU 线程。 有关详细信息，请参见:

- [使用“并行堆栈”窗口](../debugger/using-the-parallel-stacks-window.md)

- [使用“任务”窗口](../debugger/using-the-tasks-window.md)

- [如何：使用“并行监视”窗口](../debugger/how-to-use-the-parallel-watch-window.md)

- [调试线程和进程](../debugger/debug-threads-and-processes.md)（调试位置工具栏）

- [如何：使用“GPU 线程”窗口](../debugger/how-to-use-the-gpu-threads-window.md)

## <a name="data-synchronization-exceptions"></a>数据同步异常
 调试器可以在执行期间标识多个数据同步条件。 在检测条件时，调试器会进入中断状态。 有两个选项：“中断”或“继续”。 通过使用“异常”对话框，可以配置调试器是否检测这些条件以及它将在哪些条件下中断。 有关详细信息，请参阅[在调试器中管理异常](../debugger/managing-exceptions-with-the-debugger.md)。 还可以使用“选项”对话框来指定调试器应忽略异常（如果写入的数据不更改数据的值）。 有关更多信息，请参见 [General, Debugging, Options Dialog Box](../debugger/general-debugging-options-dialog-box.md)。

## <a name="troubleshooting"></a>疑难解答

### <a name="specifying-an-accelerator"></a>指定加速器
 如果代码在 [accelerator::direct3d_ref](/cpp/parallel/amp/reference/accelerator-class#direct3d_ref) (REF) 加速器上运行，则仅命中 GPU 代码中的断点。 如果未指定代码中的加速器，则自动将 REF 加速器选作项目属性中的“调试加速器类型”。 如果你的代码显式选择加速器，则在调试期间将不会使用 REF 加速器，并且将不会命中断点，除非你的 GPU 硬件具有调试支持。 你可以通过编写代码来对此情况进行补救，以便在调试期间使用 REF 加速器。 有关详细信息，请参阅项目属性和[使用加速器和 Accelerator_view 对象](/cpp/parallel/amp/using-accelerator-and-accelerator-view-objects)以及[用于C++调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

### <a name="conditional-breakpoints"></a>条件断点
 GPU 代码中的条件断点是受支持的，但并不能在设备上计算所有表达式。 当无法在设备上计算某个表达式时，将在调试器中计算该表达式。 调试器的运行速度比设备的运行速度慢得多。

### <a name="error-there-is-a-configuration-issue-with-the-selected-debugging-accelerator-type"></a>错误：选定的调试加速器类型存在配置问题。
 当项目设置和您在其上进行调试的 PC 的配置之间存在不一致之处时，会发生此错误。 有关详细信息，请参阅[ C++调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

### <a name="error-the-debug-driver-for-the-selected-debugging-accelerator-type-is-not-installed-on-the-target-machine"></a>错误：目标计算机上未安装选定的调试加速器类型的调试驱动程序。
 如果在远程 PC 上进行调试，则会发生此错误。 调试器无法确定远程 PC 上是否安装了驱动程序，直到运行时。 可从图形卡的制造商处获得驱动程序。

### <a name="error-timeout-detection-and-recovery-tdr-must-be-disabled-at-the-remote-site"></a>错误：必须在远程站点上禁用超时检测和恢复 (TDR)。
 C++ AMP 计算可能会超过由 Windows 超时检测和恢复进程 (TDR) 设置的默认时间间隔。 在这种情况下，计算将被取消，并且数据将丢失。 有关详细信息，请参阅[在 C++ AMP 中处理 TDR](http://go.microsoft.com/fwlink/p/?LinkId=249154)。

## <a name="see-also"></a>请参阅
- [演练：调试 C++ AMP 应用程序](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [在 Visual Studio 中开始 GPU 调试](http://go.microsoft.com/fwlink/p/?LinkId=255381)