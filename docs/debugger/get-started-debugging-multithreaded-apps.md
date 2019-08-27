---
title: 了解如何调试多线程应用程序
description: 使用 Visual Studio 中的并行堆栈和并行监视窗口进行调试
ms.custom: ''
ms.date: 11/16/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- multithreaded debugging, tutorial
- tutorials, multithreaded debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f07791a02c5e84722e8193f21b7ed2fe37bdd7f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849612"
---
# <a name="get-started-debugging-multithreaded-applications-c-visual-basic-c"></a>开始调试多线程应用程序 (C#，Visual Basic 中， C++)

Visual Studio 提供多种工具和用户界面元素，用于调试多线程应用程序。 本教程演示如何使用线程标记、“并行堆栈”  窗口、“并行监视”  窗口、条件断点、筛选器断点。 完成本教程只需数分钟，然后你就会熟悉用于调试多线程应用程序的功能。

下面两个主题额外介绍了如何使用其他多线程调试工具：

- 若要使用**调试位置**工具栏和**线程**窗口中，请参阅[演练：调试多线程应用程序](../debugger/how-to-use-the-threads-window.md)。

- 有关使用的示例<xref:System.Threading.Tasks.Task>（托管代码） 和并发运行时 (C++)，请参阅[演练：调试并行应用程序](../debugger/walkthrough-debugging-a-parallel-application.md)。 有关适用于大多数多线程应用程序类型的常规调试技巧，请阅读该主题和本主题。

首先需要一个多线程应用程序项目。 示例如下。

## <a name="create-a-multithreaded-app-project"></a>创建一个多线程应用项目

1. 打开 Visual Studio 并创建一个新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 类型**Ctrl + Q**若要打开搜索框中，键入**控制台**(或**c + +** )，选择**模板**，，然后：

    - 有关C#或 Visual Basic 中，选择**创建新的控制台应用 (.NET Framework) 项目**为C#或 Visual Basic。 在出现的对话框中，选择“创建”  。
    - 有关C++，选择**创建新的控制台应用项目**为C++。 在出现的对话框中，选择“创建”  。

    然后，键入一个名称，如**MyThreadWalkthroughApp**然后单击**创建**。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在顶部菜单栏，依次选择“文件”   > “新建”   > “项目”  。 在左窗格中**新的项目**对话框框中，选择以下：

    - 有关C#应用程序下**可视化C#** ，选择**Windows 桌面**，然后在中间窗格中选择**控制台应用 (.NET Framework)** 。
    - 对于 Visual Basic 应用，在**Visual Basic**，选择**Windows Desktop**，然后在中间窗格中选择**控制台应用 (.NET Framework)** 。
    - 有关C++应用程序下**可视化C++** ，选择**Windows 桌面**、，然后选择**Windows 控制台应用程序**。

    然后，键入一个名称，如**MyThreadWalkthroughApp**然后单击**确定**。
    ::: moniker-end

    如果没有看到“控制台应用”项目模板，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序    。 选择“.NET 桌面开发”或“使用 C++ 的桌面开发”工作负载，然后选择“修改”    。

1. 选择 **确定**。

    新的控制台项目随即显示。 创建该项目后，将显示源文件。 根据所选语言，源文件名称可能是 Program.cs、MyThreadWalkthroughApp.cpp 或 Module1.vb    。

1. 删除出现在源文件中的代码，将其替换为下面列出的相应示例代码。

    ```csharp
    using System;
    using System.Threading;

    public class ServerClass
    {

        static int count = 0;
        // The method that will be called when the thread is started.
        public void InstanceMethod()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");

            int data = count++;
            // Pause for a moment to provide a delay to make
            // threads more apparent.
            Thread.Sleep(3000);
            Console.WriteLine(
                "The instance method called by the worker thread has ended.");
        }
    }

    public class Simple
    {
        public static void Main()
        {
            for (int i = 0; i < 10; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();

            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.InstanceMethod));
            // Start the thread.
            InstanceCaller.Start();

            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");

        }
    }
    ```

    ```C++
    #include "pch.h"
    #include <thread>
    #include <iostream>
    #include <vector>

    int count = 0;

    void doSomeWork() {

        std::cout << "The doSomeWork function is running on another thread." << std::endl;
        int data = count++;
        // Pause for a moment to provide a delay to make
        // threads more apparent.
        std::this_thread::sleep_for(std::chrono::seconds(3));
        std::cout << "The function called by the worker thread has ended." << std::endl;
    }

    int main() {
        std::vector<std::thread> threads;

        for (int i = 0; i < 10; ++i) {

            threads.push_back(std::thread(doSomeWork));
            std::cout << "The Main() thread calls this after starting the new thread" << std::endl;
    }

    for (auto& thread : threads) {
        thread.join();
    }

    return 0;
    }
    ```

    ```VB
    Imports System.Threading

    Public Class ServerClass
        ' The method that will be called when the thread is started.
        Public count = 0
        Public Sub InstanceMethod()
            Console.WriteLine(
                    "ServerClass.InstanceMethod is running on another thread.")

            Dim data = count + 1
            ' Pause for a moment to provide a delay to make
            ' threads more apparent.
            Thread.Sleep(3000)
            Console.WriteLine(
                    "The instance method called by the worker thread has ended.")
        End Sub

    End Class

    Public Class Simple

        Public Shared Sub Main()

            Dim ts As New ThreadStarter
            For index = 1 To 10
                ts.CreateThreads()
            Next

        End Sub

    End Class
    Public Class ThreadStarter
        Public Sub CreateThreads()
            Dim serverObject As New ServerClass()

            ' Create the thread object, passing in the
            ' serverObject.InstanceMethod method using a
            ' ThreadStart delegate.
            Dim InstanceCaller As New Thread(AddressOf serverObject.InstanceMethod)

            ' Start the thread.
            InstanceCaller.Start()

            Console.WriteLine("The Main() thread calls this after " _
                        + "starting the new InstanceCaller thread.")

        End Sub
    End Class
    ```

1. 在“文件”  菜单上，单击“全部保存”  。

1. (仅限 Visual Basic)在解决方案资源管理器 （右窗格），右键单击项目节点，选择**属性**。 下**应用程序**选项卡上，更改**启动对象**到**简单**。

## <a name="debug-the-multithreaded-app"></a>调试多线程应用程序

1. 在源代码编辑器中，查找以下代码段之一：

    ```csharp
    Thread.Sleep(3000);
    Console.WriteLine();
    ```

    ```C++
    std::this_thread::sleep_for(std::chrono::seconds(3));
    std::cout << "The function called by the worker thread has ended." << std::endl;
    ```

    ```VB
    Thread.Sleep(3000)
    Console.WriteLine()
    ```

1. 左键单击中的左滚动条槽`Thread.Sleep`或`std::this_thread::sleep_for`语句将新断点。

    滚动条槽中的红色圆圈指示在此位置设置断点。

2. 在“调试”  菜单上，单击“开始调试(F5)”   。

    Visual Studio 将生成该解决方案，应用在附加了调试器的情况下开始运行，然后在断点处停止。

3. 在源代码编辑器中，找到包含该断点的行。

### <a name="ShowThreadsInSource"></a>发现线程标记  

1. 在调试工具栏中，单击“在源中显示线程”  按钮![在源中显示线程](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker")。

2. 按一下 **F11** 使调试器前进一个代码行。

3. 查看窗口左侧的滚动条槽。 在此行中，会看到线程标记  图标![线程标记](../debugger/media/dbg-thread-marker.png "ThreadMarker") ，类似于一条双绞线。 线程标记指示线程在此位置停止。

    线程标记可以被断点部分隐藏。

4. 将指针悬停在线程标记上。 此时会出现一个数据提示，告知你每个已停止线程的名称和线程 ID 号。 在这种情况下，名称可能是 `<noname>`。

5. 选择线程标记，以查看快捷菜单上的可用选项。

### <a name="ParallelStacks"></a>查看线程位置

在“并行堆栈”  窗口中，可以在“线程”视图和“任务”视图（适用于基于任务的编程）之间进行切换，并且可以查看每个线程的调用堆栈信息。 在此应用中，我们可以使用“线程”视图。

1. 通过选择“调试” > “窗口” > “并行堆栈”   ，打开“并行堆栈”   窗口。 此时会看到如下所示的内容。 确切信息取决于每个线程的当前位置、硬件以及编程语言。

    ![并行堆栈窗口](../debugger/media/dbg-multithreaded-parallel-stacks.png "ParallelStacksWindow")

    在此示例中，从左到右会看到托管代码的以下信息：

    - 主线程（左侧）已停止在 `Thread.Start` 上，由线程标记图标指示停止点![线程标记](../debugger/media/dbg-thread-marker.png "ThreadMarker")。
    - 两个线程已进入 `ServerClass.InstanceMethod`，其中一个线程是当前线程（黄色箭头），另一个线程已停止在 `Thread.Sleep` 中。
    - 新线程（右侧）也已启动，但是停止在 `ThreadHelper.ThreadStart` 上。

2. 右键单击“并行堆栈”  窗口中的条目，查看快捷菜单上的可用选项。

    可以通过这些右键单击菜单执行各种操作，但在本教程中，我们将在“并行监视”  窗口中展示更多这些细节（后续部分）。

    > [!NOTE]
    > 若要查看包含每个线程的信息的列表视图，请改用“线程”  窗口。 请参阅[演练：调试多线程应用程序](../debugger/how-to-use-the-threads-window.md)。

### <a name="set-a-watch-on-a-variable"></a>对变量设置监视

1. 通过选择“调试”   > “窗口”   > “并行监视”   > “并行监视 1”  ，打开“并行监视”窗口  。

2. 选择 `<Add Watch>` 文本所在的单元格（或第 4 列中的空标头单元格），输入 `data`。

    在窗口中显示每个线程的数据变量的值。

3. 选择 `<Add Watch>` 文本所在的单元格（或第 5 列中的空标头单元格），输入 `count`。

    窗口中会显示每个线程的 `count` 变量的值。 如果看不到这么多的信息，请尝试按 **F11** 几次以继续在调试器中执行线程。

    ![并行监视窗口](../debugger/media/dbg-multithreaded-parallel-watch.png "ParallelWatchWindow")

4. 右键单击其中一个窗口以查看可用选项中的行。

### <a name="flag-and-unflag-threads"></a>标记线程和取消标记线程
可以通过标记线程来追踪重要的线程，并忽略其它线程。

1. 在中**并行监视**窗口中，按住**Shift**键并选择多个行。

2. 右键单击并选择**标志**。

    所选的所有线程都将都标记。 现在，您可以筛选为仅显示已标记的线程。

3. 在中**并行监视**窗口中，选择**仅显示标记的线程**按钮![显示已标记线程](../debugger/media/dbg-threads-show-flagged.png "ThreadMarker")。

    标记的线程显示在列表中。

    > [!TIP]
    > 在标记一些线程后，可以右键单击代码编辑器中的代码行，然后选择“将标记的线程运行到光标处”  。 请确保选择所有已标记的线程将达到的代码。 Visual Studio 将在选择的代码行处暂停线程，这样就可以通过[冻结和解冻线程](#bkmk_freeze)更容易地控制执行顺序。

4. 选择**仅显示标记的线程**按钮将再次切换回**显示所有线程**模式。

5. 若要取消标记线程，请在“并行监视”  窗口右键单击一个或多个已标记线程，然后选择“取消标记”  。

### <a name="bkmk_freeze"></a> 冻结和解冻线程执行

> [!TIP]
> 可以通过冻结和解冻（暂停和恢复）线程来控制线程执行工作的顺序。 这有助于解决并发问题，例如死锁和争用条件。

1. 在“并行监视”  窗口中，在选中所有行的情况下，右键单击并选择“冻结”  。

    在第二个列中，每个行出现一个暂停图标。 暂停图标指示该线程已冻结。

2. 仅选择一行，取消选中其他行。

3. 右键单击某一行，然后选择**解冻**。

    暂停图标在此行上消失，表明线程已不再被冻结。

4. 切换到代码编辑器，按 **F11**。 仅运行未冻结的线程。

    应用还实例化某些新线程。 任何新线程均处于未标记状态，不会被冻结。

### <a name="bkmk_follow_a_thread"></a> 请按照具有条件断点的单一线程

可以在调试器中对单线程的执行情况进行跟踪。 一种方法是冻结不感兴趣的线程。 在某些情况下，可能需要在不冻结其它线程的情况下跟踪单个线程，例如重现特定 Bug。 若要在不冻结其他线程的情况下跟踪某个线程，必须避免在不感兴趣的线程上中断。 您可以执行此操作通过设置[条件断点](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)。

可以根据不同的条件（例如，线程名称或线程 ID）来设置断点。 如果你知道数据对于每个线程都是唯一的，则可根据该数据设置条件断点。 这是常见的调试场景，即相比于特定的线程，你对某些特定的数据值更感兴趣。

1. 右键单击以前创建的断点并选择**条件**。

2. 在“断点设置”  窗口中，输入 `data == 5` 作为条件表达式。

    ![条件断点](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint")

    > [!TIP]
    > 如果对特定的线程更感兴趣，则请使用线程名称或线程 ID 作为条件。 若要在“断点设置”  窗口中执行此操作，请选择“筛选器”  而不是“条件表达式”  ，并按照筛选器提示操作。 可能需要在应用代码中指定线程名称，因为线程 ID 在重启调试器时会更改。

3. 关闭**断点设置**窗口。

4. 选择重启![重启应用](../debugger/media/dbg-tour-restart.png "RestartApp")按钮以重启调试会话。

    将在数据变量的值为 5 的线程中，中断代码执行。 请在“并行监视”  窗口中，寻找表示当前调试器上下文的黄色箭头。

5. 现在，可以单步执行代码 (**F10**) 和单步执行代码 (**F11**) 并按照单个线程执行。

    只要断点条件是唯一的线程，且调试器不会命中 （可能需要禁用它们） 的其他线程上的任何其他断点，可以单步执行代码并单步执行代码而无需切换到其他线程。

    > [!NOTE]
    > 当您推进调试器进度时，将运行所有线程。 但是，调试器不会中断到其他线程上的代码中，除非其中一个其他线程遇到断点。

## <a name="see-also"></a>请参阅

- [调试多线程应用](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [如何：在调试时切换到另一个线程](../debugger/how-to-switch-to-another-thread-while-debugging.md)
- [如何：使用并行堆栈窗口](../debugger/using-the-parallel-stacks-window.md)
- [如何：使用“并行监视”窗口](../debugger/how-to-use-the-parallel-watch-window.md)