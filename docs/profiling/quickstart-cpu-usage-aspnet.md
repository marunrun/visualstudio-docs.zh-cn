---
title: 分析 CPU 使用情况数据 (ASP.NET Core)
description: 使用 CPU 使用情况诊断工具衡量 ASP.NET Core 应用中的应用性能
ms.custom: mvc
ms.date: 02/14/2020
ms.topic: quickstart
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 367d789513e8ac220566cb4e451bcea015ec5a2a
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77275080"
---
# <a name="quickstart-analyze-cpu-usage-data-in-visual-studio-aspnet-core"></a>快速入门：在 Visual Studio 中分析 CPU 使用率数据 (ASP.NET Core)

Visual Studio 提供了许多强大的功能来帮助你分析应用程序中的性能问题。 本主题提供了一种快速了解部分基本功能的方法。 此处，我们将了解用来确定由于 CPU 使用率高而导致性能瓶颈的工具。 Visual Studio 中的 .NET 开发（包括 ASP.NET、和本机 /C++ 开发）支持此诊断工具。

诊断中心提供了大量其他选项来运行和管理诊断会话。 如果此处介绍的“CPU 使用率”  工具未提供所需数据，[其他分析工具](../profiling/profiling-feature-tour.md)可提供可能有帮助的不同种类的信息。 在许多情况下，CPU 以外的因素可能会导致应用程序性能瓶颈，例如内存、呈现 UI 或网络请求时间。

要运行带调试器的分析工具（“诊断工具”窗口），需具备 Windows 8 及更高版本  。 在 Windows 7 及更高版本中，可使用事后分析工具（即[性能探查器](../profiling/profiling-feature-tour.md)）。

## <a name="create-a-project"></a>创建项目

1. 打开 Visual Studio 并创建项目。

   ::: moniker range="vs-2017"
   从顶部菜单栏中选择“文件”>“新建”>“项目”    。

   在“新建项目”对话框的左窗格中，展开“Visual C#”，然后选择“Web”    。 在中间窗格中，选择“ASP.NET Web 应用程序(.NET Core)”  。 然后将该项目命名为 MyProfilingApp_MVC  。

   > [!NOTE]
   > 如果没有看到“ASP.NET Web 应用程序(.NET Core)”项目模板，请选择“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接    。 Visual Studio 安装程序启动。 选择“ASP.NET 和 Web 开发”工作负载，然后选择“修改”   。

   在显示的对话框中，选择中间窗格中的“MVC”  ，然后单击“确定”  。
   ::: moniker-end
   ::: moniker range="vs-2019"
   如果开始窗口未打开，请选择“文件”>“开始窗口”   。

   在“开始”窗口上，选择“创建新项目”  。

   在“创建新项目”窗口中，在搜索框中输入或键入“asp.net”   。 接下来，从“语言”列表中选择 C#，然后从“平台”列表中选择 Windows   。

   应用语言和平台筛选器之后，选择“ASP.NET Web 应用程序(.NET Core)”模板，然后选择“下一步”   。

   > [!NOTE]
   > 如果未看到“ASP.NET Web 应用程序(.NET Core)”模板，则可以从“创建新项目”窗口安装该模板   。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。 然后，在 Visual Studio 安装程序中，选择“ASP.NET 和 Web 开发”工作负载  。

   在“配置新项目”窗口中，在“项目名称”框中键入或输入“MyProfilingApp_MVC”    。 然后，选择“创建”  。

   在出现的窗口中，选择“Web 应用程序(模型-视图-控制器)”，然后选择“创建”   。

   ::: moniker-end

   此时，Visual Studio 将打开新项目。

1. 在解决方案资源管理器中右键单击“模型”文件夹，然后选择“添加”   > “类”  。

1. 将新类命名为 `Data.cs` 并选择“添加”  。

1. 在解决方案资源管理器中，打开 `Models/Data.cs` 并将以下 `using` 语句添加到文件顶部：

    ```csharp
    using System.Threading;
    ```

1. 在 Data.cs 中，将以下代码：

    ```csharp
    public class Data
    {
    }
    ```

    替换为此代码：

    ```csharp
    public class ServerClass
    {
        const int MIN_ITERATIONS = int.MaxValue / 1000;
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;

        long m_totalIterations = 0;
        readonly object m_totalItersLock = new object();
        // The method that will be called when the thread is started.
        public void GenerateData()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");

            var x = GetNumber();
        }

        private int GetNumber()
        {
            var rand = new Random();
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);
            var result = 0;
            lock (m_totalItersLock)
            {
                m_totalIterations += iters;
            }
            // we're just spinning here
            // and using Random to frustrate compiler optimizations
            for (var i = 0; i < iters; i++)
            {
                result = rand.Next();
            }
            return result;
        }
    }

    public class Simple
    {
        int numberOfThreads = 200;

        public Simple()
        {
            for (int i = 0; i < numberOfThreads; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();

            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.GenerateData));
            // Start the thread.
            InstanceCaller.Start();

            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");

        }

        public int GetData()
        {
            // Not returning any meaningful data.
            return numberOfThreads;
        }
    }
    ```

1. 在“解决方案资源管理器”中，打开“Controller/HomeControllers.cs”  ，并将以下代码：

   ::: moniker range="vs-2017"

    ```csharp
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";

        return View();
    }
    ```

    替换为此代码：

    ```csharp
    public ActionResult About()
    {
        Models.Simple s = new Models.Simple();

        ViewBag.Message = "Your application description page.";

        return View(s.GetData());
    }
    ```

    ::: moniker-end
    ::: moniker range="vs-2019"

    ```csharp
    public IActionResult Privacy()
    {
        return View();
    }
    ```

    替换为此代码：

    ```csharp
    public IActionResult Privacy()
    {
        Models.Simple s = new Models.Simple();

        return View(s.GetData());
    }
    ```

    ::: moniker-end


## <a name="step-1-collect-profiling-data"></a>步骤 1：收集分析数据

1. 首先，在应用中在 `Simple` 构造函数的该代码行处设置一个断点：

    `for (int i = 0; i < 200; i++)`

    单击代码行左侧的装订线，设置断点。

1. 然后，在 `Simple` 构造函数末尾的右括号处设置第二个断点：

     ![设置断点以进行分析](../profiling/media/quickstart-cpu-usage-breakpoints-aspnet.png)

    > [!TIP]
    > 通过设置两个断点，可将数据收集限制到想要分析的代码部分。

1. 已显示“诊断工具”  窗口，除非已将其关闭。 若要再次显示该窗口，请依次单击“调试”   > “Windows”   > “显示诊断工具”  。

1. 依次单击“调试”   > “启动调试”  或单击工具栏上的“启动”  或按 F5  。

1. 应用加载完成后，单击网页顶部的适当链接，开始运行新代码。

   ::: moniker range="vs-2017"
   在 Visual Studio 2017 中，单击“关于”链接以运行代码  。
   ::: moniker-end
   ::: moniker range="vs-2019"
   在 Visual Studio 2019 中，单击“隐私”链接以运行代码  。
   ::: moniker-end

1. 查看显示的诊断工具的“摘要”  视图。

1. 调试器暂停时，选择“记录 CPU 配置文件”  以启用 CPU 使用率数据的收集，然后打开“CPU 使用率”  选项卡。

     ![诊断工具启用 CPU 分析](../profiling/media/quickstart-cpu-usage-summary.png)

     启用数据收集时，记录按钮将显示一个红圈。

     选择“记录 CPU 配置文件”  时，Visual Studio 将开始记录函数和执行函数所花的时间，还会提供一个时间线关系图，可使用此关系图专注于采样会话的特定分段。只有应用程序在断点处停止时，才可以查看该收集数据。

6. 按 F5 将应用运行到第二个断点。

     现在将拥有应用程序特定于在两个断点间运行的代码区域的性能数据。

     探查器开始准备线程数据。 等待其完成。

     CPU 使用率工具在“CPU 使用率”  选项卡中显示报表。

     现在可以开始分析数据。

## <a name="step-2-analyze-cpu-usage-data"></a>步骤 2：分析 CPU 使用量数据

建议通过检查 CPU 使用率下的函数列表开始分析数据，然后确定执行大部分工作的函数，最后仔细查看每一个函数。

1. 在函数列表中，检查执行大部分工作的函数。

     ![诊断工具“CPU 使用率”选项卡](../profiling/media/quickstart-cpu-usage-cpu-aspnet.png)

    > [!TIP]
    > 函数将按执行工作量从多到少排列（不按调用顺序）。 这有助于快速标识运行时间最长的函数。

2. 在函数列表中，双击 `MyProfilingApp_MVC.Models.ServerClass::GetNumber` 函数。

    双击该函数时，将在左侧窗格中打开“调用方/被调用方”  视图。

    ![诊断工具“调用方和被调用方”视图](../profiling/media/quickstart-cpu-usage-caller-callee-aspnet.png)

    在此视图中，所选函数显示在标题和“当前函数”  框中（本例中为 `ServerClass::GetNumber`）。 调用当前函数的函数显示在左侧的“调用函数”  中，当前函数调用的任何函数均显示在右侧的“被调用函数”  框中。 （可选择其中一个框来更改当前函数。）

    此视图显示总时间及函数完成执行所用的总体应用运行时间的百分比。

    **函数体**还显示函数体中所用的时间总量（及百分比），其中不包括调用和被调用函数中所用的时间。 （在此图中，共花费 2235 毫秒，函数体内花费 2220 毫秒，其余时间（<20 毫秒）花费在此函数调用的外部代码中）。 环境不同，实际值也不同。

    > [!TIP]
    > **函数体**中的较高值可能指示函数自身内部的性能瓶颈。

## <a name="next-steps"></a>后续步骤

- [分析内存使用量](../profiling/memory-usage.md)，确定性能瓶颈。
- [分析 CPU 使用情况](../profiling/cpu-usage.md)，更深入地了解 CPU 使用率工具。
- 在不附加调试程序的情况下，或通过将正在运行的应用作为目标来分析 CPU 使用率。有关详细信息，请参阅[在使用或不使用调试程序的情况下运行分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)中的[在不使用调试程序的情况下收集分析数据](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging)。

## <a name="see-also"></a>请参阅

- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
