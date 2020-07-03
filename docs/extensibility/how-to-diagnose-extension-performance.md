---
title: 如何：诊断扩展性能 |Microsoft Docs
ms.date: 11/08/2016
ms.topic: how-to
ms.assetid: 46b0a1e3-7e69-47c9-9d8d-a1815d6c3896
author: BertanAygun
ms.author: bertaygu
manager: jillfra
ms.workload:
- bertaygu
ms.openlocfilehash: 542d8a6d6d90091aa7a800ef18f847fea6b1a81c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905910"
---
# <a name="measuring-extension-impact-in-startup"></a>度量扩展对启动的影响

## <a name="focus-on-extension-performance-in-visual-studio-2017"></a>专注于 Visual Studio 2017 中的扩展性能

根据客户反馈，Visual Studio 2017 版本的重点领域之一是启动和解决方案加载性能。 作为 Visual Studio 平台团队，我们一直致力于改进启动和解决方案加载性能。 通常，我们的度量值建议安装的扩展还会对这些方案产生相当大的影响。

为了帮助用户了解这一影响，我们在 Visual Studio 中添加了一项新功能，通知用户的扩展速度缓慢。 有时，Visual Studio 会检测到一个新扩展，该扩展会减缓解决方案加载或启动的速度。 检测到缓慢时，用户会在 IDE 中看到一条指向新的 "管理 Visual Studio 性能" 对话框的通知。 还可以通过 "帮助" 菜单访问此对话框，以浏览以前检测到的扩展。

![管理 Visual Studio 性能](media/manage-performance.png)

本文档旨在通过说明如何计算扩展影响来帮助扩展开发人员。 本文档还介绍了如何在本地分析扩展影响。 本地分析扩展影响将确定扩展是否可能显示为性能影响的扩展。

> [!NOTE]
> 本文档重点介绍扩展对启动和解决方案加载的影响。 当扩展导致 UI 无响应时，它们也会影响 Visual Studio 性能。 有关本主题的详细信息，请参阅[如何：诊断由扩展引起的 UI 延迟](how-to-diagnose-ui-delays-caused-by-extensions.md)。

## <a name="how-extensions-can-impact-startup"></a>扩展如何影响启动

对于扩展对启动性能的影响，最常见的一种方法是选择在某个已知启动 UI 上下文（如 NoSolutionExists 或 ShellInitialized）上自动加载。 这些 UI 上下文在启动过程中被激活。 `ProvideAutoLoad`此时将加载并初始化包含这些上下文的定义中包含属性的所有包。

当我们度量扩展的影响时，我们主要重点介绍那些选择在上述上下文中自动加载的扩展所花费的时间。 度量时间包括但不限于：

* 为同步包加载扩展程序集
* 用于同步包的包类构造函数中花费的时间
* 同步包的包初始化（或 SetSite）方法所用的时间
* 对于异步包，以上操作在后台线程上运行。  因此，不会监视这些操作。
* 在包初始化期间计划在主线程上运行的任何异步工作所用的时间
* 事件处理程序所用的时间，特别是 shell 初始化上下文激活或 shell 傀儡状态更改
* 从 Visual Studio 2017 Update 3 开始，还会在初始化 shell 之前开始监视空闲调用所用的时间。 空闲处理程序中的长时间操作还会导致未响应的 IDE，并导致用户看到的启动时间。

从 Visual Studio 2015 开始，我们添加了许多功能。 这些功能有助于消除包自动加载的需求。 这些功能还可将包加载的需求推迟到更具体的情况。 这些情况包括一些示例，用户在自动加载时更需要使用该扩展或降低扩展影响。

可在以下文档中找到有关这些功能的更多详细信息：

[基于规则的 ui 上下文](how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)：围绕 ui 上下文构建的基于规则的更丰富的引擎使你可以基于项目类型、风格和属性创建自定义上下文。 自定义上下文可用于在更具体的方案中加载包。 这些特定方案包括具有特定功能（而不是启动）的项目。 自定义上下文还允许基于项目组件或其他可用字词[将命令可见性绑定到自定义上下文](visibilityconstraints-element.md)。 此功能无需加载包即可注册命令状态查询处理程序。

[异步包支持](how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)： visual studio 2015 中的新 AsyncPackage 基类允许在自动加载属性或异步服务查询请求包负载时，以异步方式在后台加载 Visual studio 包。 此后台加载允许 IDE 保持响应。 即使扩展在后台和关键方案（如启动和解决方案加载）中初始化时，IDE 也能响应。

[异步服务](how-to-provide-an-asynchronous-visual-studio-service.md)：通过异步包支持，我们还添加了对异步查询服务的支持并能够注册异步服务。 更重要的是，我们正在转换核心 Visual Studio 服务以支持异步查询，以便异步查询中的大部分工作都在后台线程中进行。 SComponentModel （Visual Studio MEF 主机）是现在支持异步查询以允许扩展完全支持异步加载的主要服务之一。

## <a name="reducing-impact-of-auto-loaded-extensions"></a>减少自动加载的扩展的影响

如果包仍需要在启动时自动加载，则很重要的一点是将包初始化过程中完成的工作降到最低。 最大程度地降低包初始化工作可降低扩展影响启动的几率。

可能导致包初始化开销较高的一些示例如下：

### <a name="use-of-synchronous-package-load-instead-of-asynchronous-package-load"></a>使用同步包加载，而不是异步包加载

由于默认情况下，会在主线程上加载同步包，因此我们鼓励具有自动加载包的扩展所有者改用异步包基类，如前文所述。 更改自动加载的包以支持异步加载还可以更轻松地解决下面的其他问题。

### <a name="synchronous-filenetwork-io-requests"></a>同步文件/网络 IO 请求

理想情况下，应避免在主线程中进行任何同步文件或网络 IO 请求。 它们的影响将取决于计算机状态，并且在某些情况下可能会在很长一段时间内阻塞。

使用异步包加载和异步 IO Api 应确保包初始化在这种情况下不会阻止主线程。 用户还可以继续与 Visual Studio 交互，同时在后台发生 i/o 请求。

### <a name="early-initialization-of-services-components"></a>服务、组件的早期初始化

包初始化中的一种常见模式是在包或方法中初始化此包使用或提供的服务 `constructor` `initialize` 。 虽然这可确保服务可供使用，但如果不立即使用这些服务，它也可能会增加不必要的包加载成本。 相反，应按需初始化此类服务，以最大程度地减少在包初始化中完成的工作。

对于包提供的全局服务，可以使用 `AddService` 方法，该方法仅在组件请求服务时才会延迟初始化该服务。 对于包中使用的服务，可以使用延迟 \<T> 或 AsyncLazy \<T> 来确保首次使用时初始化/查询服务。

## <a name="measuring-impact-of-auto-loaded-extensions-using-activity-log"></a>使用活动日志度量自动加载的扩展的影响

从 Visual Studio 2017 Update 3 开始，Visual Studio 活动日志现在包含在启动和解决方案加载过程中对包的性能影响的条目。 若要查看这些度量值，必须打开带有/log 开关的 Visual Studio 并打开*ActivityLog.xml*文件。

在活动日志中，条目将位于 "管理 Visual Studio 性能" 源下，并将如以下示例所示：

```Component: 3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c, Inclusive Cost: 2008.9381, Exclusive Cost: 2008.9381, Top Level Inclusive Cost: 2008.9381```

此示例显示，在 Visual Studio 启动时，GUID 为 "3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c" 的包花费了 2008 ms。 请注意，当计算某个包的影响时，Visual Studio 会将顶级成本视为主要数字，因为这是用户在禁用该包的扩展时看到的节省量。

## <a name="measuring-impact-of-auto-loaded-extensions-using-perfview"></a>使用 PerfView 度量自动加载的扩展的影响

尽管代码分析有助于识别可能会减慢包初始化速度的代码路径，但你也可以使用 PerfView 等应用程序来利用跟踪，以了解在 Visual Studio 启动过程中包加载的影响。

PerfView 是系统范围内的跟踪工具。 此工具可帮助你了解应用程序中的热路径，原因可能是 CPU 使用率或阻塞系统调用。 下面是使用[Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=28567)提供的 PerfView 分析示例扩展的快速示例。

**示例代码：**

此示例基于下面的示例代码，该代码旨在显示某些常见延迟导致的情况：

```csharp
protected override void Initialize()
{
    // Initialize a class from another assembly as an example
    MakeVsSlowServiceImpl service = new MakeVsSlowServiceImpl();

    // Costly work in main thread involving file IO
    string systemPath = Environment.GetFolderPath(Environment.SpecialFolder.Windows);
    foreach (string file in Directory.GetFiles(systemPath))
    {
        DateTime creationDate = File.GetCreationTime(file);
    }

    // Costly work after shell is initialized. This callback executes on main thread
    KnownUIContexts.ShellInitializedContext.WhenActivated(() =>
    {
        DoMoreWork();
    });

    // Start async work on background thread
    DoAsyncWork().Forget();
}

private async Task DoAsyncWork()
{
    // Switch to background thread to do expensive work
    await TaskScheduler.Default;
    System.Threading.Thread.Sleep(500);
}

private void DoMoreWork()
{
    // Costly work
    System.Threading.Thread.Sleep(500);
    // Blocking call to an asynchronous work.
    ThreadHelper.JoinableTaskFactory.Run(async () => { await DoAsyncWork(); });
}
```

**使用 PerfView 记录跟踪：**

设置了安装了扩展的 Visual Studio 环境后，可以通过打开 PerfView 并从 "**收集**" 菜单打开 "**收集**" 对话框来记录启动跟踪。

![perfview 收集菜单](media/perfview-collect-menu.png)

默认选项将为 CPU 消耗提供调用堆栈，但由于我们对阻塞时间感兴趣，因此还应启用**线程时间**堆栈。 设置准备就绪后，可以单击 "**开始收集**"，然后在录制开始后打开 Visual Studio。

在停止收集之前，你需要确保 Visual Studio 已完全初始化，主窗口完全可见，如果你的扩展具有自动显示的任何 UI 段，则它们也会可见。 完全加载 Visual Studio 并初始化扩展时，可以停止记录以分析跟踪。

**使用 PerfView 分析跟踪：**

完成记录后，PerfView 将自动打开跟踪和展开选项。

出于本示例的目的，我们主要对 "**线程时间堆栈**" 视图感兴趣，可以在 "**高级组**" 下找到此视图。 此视图将通过包括 CPU 时间和阻塞时间（如磁盘 IO 或等待句柄）的方法，显示在线程上所花费的总时间。

 ![线程时间堆栈](media/perfview-thread-time-stacks.png)

 打开 "**线程时间堆栈**" 视图时，应选择 " **devenv** " 进程开始分析。

PerfView 提供了有关如何在其自己的 "帮助" 菜单下读取线程时间堆栈的详细指南，以便进行更详细的分析。 出于本示例的目的，我们想要进一步筛选此视图，只需在包模块名称和启动线程中加入堆栈。

1. 将**GroupPats**设置为空文本可以删除默认添加的所有分组。
2. 除了现有的进程筛选器外，将**IncPats**设置为包含部分程序集名称和启动线程。 在这种情况下，它应为**devenv;启动线程;MakeVsSlowExtension**。

现在，视图将仅显示与与扩展相关的程序集关联的成本。 在此视图中，启动线程的 " **inc." （非独占成本）** 列中列出的任何时间均与筛选的扩展相关，并将影响启动。

在上面的示例中，一些有趣的调用堆栈是：

1. 使用类的 IO `System.IO` ：这些帧的非独占成本在跟踪中可能不太昂贵，因为文件 IO 速度因计算机而异。

   ![系统 io 帧](media/perfview-system-io-frames.png)

2. 等待其他异步工作的阻止调用：在这种情况下，包含时间表示在异步工作完成时主线程被阻止的时间。

   ![阻止调用帧](media/perfview-blocking-call-frames.png)

跟踪中用于确定影响的其他视图之一将是**映像加载堆栈**。 可以应用应用于 "**线程时间堆栈**" 视图的相同筛选器，并查找由于自动加载的包所执行的代码而加载的所有程序集。

将加载的程序集的数量降到最少很重要，因为每个附加的程序集都涉及额外的磁盘 i/o，这会使计算机速度变慢的启动。

## <a name="summary"></a>总结

Visual Studio 的启动是我们不断获得反馈的领域之一。 如前所述，我们的目标是让所有用户都拥有一致的启动体验，而不考虑它们所安装的组件和扩展。 我们想要与扩展所有者合作，帮助我们实现这一目标。 上述指南应该有助于理解扩展对启动的影响，并且无需以异步方式自动加载或加载它来最大程度地降低对用户工作效率的影响。
