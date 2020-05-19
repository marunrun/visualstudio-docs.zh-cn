---
title: 使用 IntelliTrace 查看事件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e1c9c91a-0009-4c4e-9b4f-c9ab3a6022a7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ffbe0b8365948dc5a69edca390f308cb55ba5a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929409"
---
# <a name="view-events-with-intellitrace-in-visual-studio-enterprise-c-visual-basic"></a>在 Visual Studio Enterprise 中使用 IntelliTrace 查看事件（C#、Visual Basic）

你可以使用 IntelliTrace 来收集关于特定事件或事件类别的信息，或收集关于除了事件外的单个函数调用的信息。 下列过程演示如何执行此操作。

可以在 Visual Studio Enterprise 版（但不可在 Professional 或 Community 版）中使用 IntelliTrace。

## <a name="configure-intellitrace"></a><a name="GettingStarted"></a> 配置 IntelliTrace

你可以尝试仅使用 IntelliTrace 事件进行调试。 IntelliTrace 事件是调试器事件、异常、.NET Framework 事件和其他系统事件。 你应在开始调试之前打开或关闭特定事件以控制 IntelliTrace 记录的事件。 有关详细信息，请参阅 [IntelliTrace 功能](../debugger/intellitrace-features.md)。

- 打开 IntelliTrace 事件以进行文件访问。 转到“工具”>“选项”>“IntelliTrace”>“IntelliTrace 事件”页，然后展开“文件”类别 。 检查 **“文件”** 事件类别。 这将导致检查所有文件事件（访问、关闭、删除）。

## <a name="create-your-app"></a>创建应用程序

1. 创建 C# 控制台应用程序。 在 Program.cs 文件中，添加以下 `using` 语句：

    ```csharp
    using System.IO;
    ```

2. 在 Main 方法中，创建 <xref:System.IO.FileStream> ，从其中进行读取、将其关闭，然后删除该文件。 添加另一行，添加该行的唯一目的是留出设置断点的位置：

    ```csharp
    static void Main(string[] args)
    {
        FileStream fs = File.Create("WordSearchInputs.txt");
        fs.ReadByte();
        fs.Close();
        File.Delete("WordSearchInputs.txt");

        Console.WriteLine("done");
    }
    ```

3. 在 `Console.WriteLine("done");`上设置断点

## <a name="start-debugging-and-view-intellitrace-events"></a>启动调试并查看 IntelliTrace 事件

1. 照常启动调试。 （按“F5”或单击“调试”>“启动调试”） 。

    > [!TIP]
    > 在调试时使“局部变量”和“自动”窗口保持打开状态，以查看并记录这些窗口中的值 。

2. 执行在断点处停止。 如果未显示“诊断工具”窗口，则单击“调试”>“Windows”>“IntelliTrace 事件” 。

    在 **“诊断工具”** 窗口中，找到 **“事件”** 选项卡（应该看到 **“事件”** 、 **“内存使用”** 和 **“CPU ”** 三个选项卡）。 **“事件”** 选项卡显示按时间排序的事件列表，以调试器中断执行之前的最后一个事件结尾。 你应会看到一个名为 **“访问 WordSearchInputs.txt”** 的事件。

    以下屏幕截图取自 Visual Studio 2015 Update 1。

    ![IntelliTrace&#45;Update1](../debugger/media/intellitrace-update1.png "IntelliTrace-Update1")

3. 选择该事件以展开其详细信息。

    以下屏幕截图取自 Visual Studio 2015 Update 1。

    ![IntelliTraceUpdate1-SingleEvent](../debugger/media/intellitraceupdate1-singleevent.png "IntelliTraceUpdate1-SingleEvent")

    你可以选择路径名链接以打开文件。 如果完整的路径名不可用，则将显示 **“打开文件”** 对话框。

    单击“激活历史调试”，这会将调试器的上下文设置为收集所选事件的时间，并且会在“调用堆栈”、“局部变量”和其他参与的调试器窗口中显示历史数据  。 如果源代码可用，则 Visual Studio 会将指针移到源窗口中的相应代码，以便你可以检查它。

    以下屏幕截图取自 Visual Studio 2015 Update 1。

    ![HistoricalDebugging-Update1](../debugger/media/historicaldebugging-update1.png "HistoricalDebugging-Update1")

4. 如果找不到 bug，请尝试检查导致 bug 的其他事件。 还可以让 IntelliTrace 记录调用信息，以便你可以单步执行函数调用。

## <a name="next-steps"></a>后续步骤

你可以将 IntelliTrace 的某些高级功能与历史调试配合使用：

- 若要查看快照，请参阅[使用 IntelliTrace 检查上一应用状态](../debugger/view-historical-application-state.md)
- 若要了解如何检查变量和导航代码，请参阅[使用历史调试检查应用](../debugger/historical-debugging-inspect-app.md)
