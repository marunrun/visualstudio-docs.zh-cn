---
title: 如何：诊断扩展性能 |Microsoft Docs
ms.date: 11/08/2016
ms.topic: conceptual
ms.assetid: 46b0a1e3-7e69-47c9-9d8d-a1815d6c3896
author: BertanAygun
ms.author: bertaygu
manager: jillfra
ms.workload:
- bertaygu
ms.openlocfilehash: 3d8fb5de23cbc4664ea322a9149653598956aed7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62863272"
---
# <a name="measuring-extension-impact-in-startup"></a>测量中启动扩展影响

## <a name="focus-on-extension-performance-in-visual-studio-2017"></a>专注于 Visual Studio 2017 中的扩展性能

根据客户反馈，Visual Studio 2017 版本的关注领域之一已被启动和解决方案负载性能。 作为 Visual Studio 平台团队，我们一直在改进启动和解决方案负载性能。 一般情况下，我们测量值表明已安装的扩展还可以在这些方案具有相当大的影响。

为了帮助用户了解在这种影响，我们在 Visual Studio 来向用户的慢速扩展通知中添加了新功能。 有时，Visual Studio 会检测速度变慢解决方案加载或启动一个新扩展。 检测到属于运行缓慢时，用户将看到指向新的"管理 Visual Studio 性能"对话框在 IDE 中的通知。 若要浏览先前检测到的扩展帮助菜单也始终可以访问此对话框。

![管理 Visual Studio 性能](media/manage-performance.png)

本文档旨在帮助扩展开发人员通过说明如何计算扩展的影响。 本文档还介绍如何本地分析扩展的影响。 本地分析扩展的影响将确定是否可以显示作为一种性能影响扩展的扩展。

> [!NOTE]
> 本文档重点介绍在启动和解决方案加载的扩展的影响。 扩展也会影响 Visual Studio 性能时它们会导致 UI 无响应。 本主题的详细信息，请参阅[如何：诊断 UI 由扩展引起的延迟](how-to-diagnose-ui-delays-caused-by-extensions.md)。

## <a name="how-extensions-can-impact-startup"></a>如何扩展可能会影响启动

扩展影响启动性能的最常见方式之一是通过选择一个已知的启动 UI 上下文，如 NoSolutionExists 或 ShellInitialized 自动加载。 在启动期间激活这些 UI 上下文。 包含的任何包`ProvideAutoLoad`会加载和初始化在该时间在其定义中使用这些上下文属性。

当我们度量值的扩展的影响时，主要侧重于通过选择在上面的上下文中自动加载这些扩展所用时间。 测量时间将包括但不是限于：

* 加载的扩展程序集的同步包
* 在包类构造函数中同步包所用的时间
* 同步的包的包初始化 （或 SetSite） 方法中所用的时间
* 对于异步包，上述操作在后台线程上运行。  在这种情况下，操作将从监视中排除。
* 计划包初始化期间主线程上运行任何异步工作中花费的时间
* 所用的事件处理程序，特别是命令行程序初始化上下文激活或 shell 僵停状态更改时间
* 从 Visual Studio 2017 Update 3 开始，我们还会监视所用的时间在空闲调用命令行程序初始化之前。 空闲处理程序中的长时间操作还会导致无响应的 IDE 和假设的启动时间，用户的贡献。

我们添加了从 Visual Studio 2015 的许多功能。 这些功能帮助消除程序包添加到自动加载的需要。 功能还推迟程序包加载到更具体的情况下需要。 这种情况下包括的用户也会更有把握，若要使用的扩展或减少扩展影响时自动加载的示例。

您可以在以下文档中找到有关这些功能的更多详细信息：

[基于规则的 UI 上下文](how-to-use-rule-based-ui-context-for-visual-studio-extensions.md):围绕 UI 上下文构建更丰富的基于规则的引擎，可创建基于项目类型、 版本和属性的自定义上下文。 自定义上下文可用于在更多特定方案期间加载的包。 这些特定的方案包括使用而不是启动某项特定功能的项目的存在。 自定义上下文还允许[命令可见性，以绑定到自定义上下文](visibilityconstraints-element.md)基于项目组件或其他可用的搜索词。 此功能消除了需要加载的包，以注册命令状态查询处理程序。

[异步程序包支持](how-to-use-asyncpackage-to-load-vspackages-in-the-background.md):Visual Studio 2015 中的新 AsyncPackage 基类允许 Visual Studio 包要加载在后台以异步方式是否请求包加载时自动加载属性或异步服务查询。 此后台加载允许 IDE 作出响应。 即使在后台中初始化该扩展和关键方案，如启动和解决方案负载不会受到影响，IDE 会快。

[异步服务](how-to-provide-an-asynchronous-visual-studio-service.md):通过异步包支持，我们还添加了对异步查询服务，并且能够进行注册的异步服务的支持。 更重要的我们正在努力将核心 Visual Studio 服务以支持异步查询，以便在后台线程中的大部分工作在异步查询中进行转换。 SComponentModel （Visual Studio MEF 主机） 是现在支持异步查询，以便支持异步加载完全扩展的主要服务之一。

## <a name="reducing-impact-of-auto-loaded-extensions"></a>减少对影响自动加载扩展

如果包仍需要将自动加载在启动时，务必最大程度减少在包初始化过程中完成的工作。 最大程度减少包初始化工作可以减少影响启动扩展的可能性。

可能会导致包初始化比较昂贵一些示例包括：

### <a name="use-of-synchronous-package-load-instead-of-asynchronous-package-load"></a>使用同步包而不是异步数据包负载的负载

因为默认情况下，可将同步包加载主线程上，我们鼓励扩展具有改为使用异步包基类如前面所述的自动加载包的所有者。 更改自动加载的包，以支持异步加载将也更加轻松地解决下面的其他问题。

### <a name="synchronous-filenetwork-io-requests"></a>同步文件/网络 IO 请求数

理想情况下应在主线程中避免任何同步的文件或网络 IO 请求。 它们的影响将取决于计算机状态，并为很长一段时间在某些情况下可以阻止。

使用异步包加载和异步 IO Api 应确保初始化的包不会阻止主线程在这种情况下。 用户还可以继续在后台中发生的 I/O 请求时使用 Visual Studio 进行交互。

### <a name="early-initialization-of-services-components"></a>早期的服务，组件初始化

一个包初始化中的常见模式是初始化由或包中的包提供的服务`constructor`或`initialize`方法。 虽然这可确保服务是可供使用，它还可以添加不必要的成本打包加载如果不立即使用这些服务。 而是应按需以最大程度减少中包初始化完成的工作已初始化此类服务。

对于提供的包的全局服务，你可以使用`AddService`采用一个函数为延迟初始化该服务，它是一个组件的请求的方法。 对于包中使用的服务，可以使用 Lazy\<T > 或 AsyncLazy\<T > 若要确保服务是在首次使用初始化/查询。

## <a name="measuring-impact-of-auto-loaded-extensions-using-activity-log"></a>测量的自动影响加载扩展使用活动日志

从 Visual Studio 2017 Update 3 开始，Visual Studio 活动日志现在将包含包的性能影响的条目启动和解决方案加载过程。 若要查看这些度量值，必须使用 /log 开关打开 Visual Studio 并打开*ActivityLog.xml*文件。

在活动日志条目将位于"管理 Visual Studio 性能"源，并看起来如下例所示：

```Component: 3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c, Inclusive Cost: 2008.9381, Exclusive Cost: 2008.9381, Top Level Inclusive Cost: 2008.9381```

此示例演示具有 GUID"3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c"的包所用的 Visual Studio 中启动 2008 ms。 请注意 Visual Studio 作为主要号码考虑顶级成本计算的包的影响，因为那是当它们禁用适用于该包的扩展时，请参阅节省用户时。

## <a name="measuring-impact-of-auto-loaded-extensions-using-perfview"></a>测量的自动影响加载使用 PerfView 的扩展

尽管代码分析可帮助识别可能会降低包初始化的代码路径，则还可以通过使用 PerfView 等应用程序以了解在 Visual Studio 启动的包负载的影响利用跟踪。

PerfView 是一个系统范围跟踪工具。 此工具将帮助您了解应用程序由于 CPU 使用率或阻止系统调用中的热路径。 下面是一个快速示例上分析一个扩展插件示例使用 PerfView 网址[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=28567)。

**示例代码：**

此示例基于示例下面的代码，旨在显示这种情况下一些常见延迟的原因：

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

**记录使用 PerfView 跟踪：**

设置后在 Visual Studio 环境与你安装的扩展，您可以通过打开 PerfView 并打开记录跟踪启动**收集**对话框从**收集**菜单。

![perfview 收集菜单](media/perfview-collect-menu.png)

默认选项将为 CPU 消耗量提供的调用堆栈，但由于我们感兴趣以及阻塞的时间，因此还应启用**线程时间**堆栈。 准备好设置后，你可以单击**开始收集**，然后开始录制后打开 Visual Studio。

停止收集之前，你想要确保完全初始化 Visual Studio，主窗口是完全可见，如果您的扩展有自动显示任何 UI 块，它们都是可见的。 Visual Studio 是完全加载和初始化您的扩展插件，可以停止录制分析跟踪。

**分析使用 PerfView 跟踪：**

完成记录后 PerfView 将自动打开跟踪并展开选项。

对于此示例的目的，我们是主要兴趣**线程时堆栈**视图可找到下**高级组**。 该视图将显示包括 CPU 时间和阻塞的时间，如磁盘 IO 或等待句柄的方法在一个线程上所花费的总时间。

 ![线程时堆栈](media/perfview-thread-time-stacks.png)

 在打开时**线程时堆栈**查看，应选择**devenv**过程以启动分析。

PerfView 提供详细指导如何阅读更详细的分析其自己帮助菜单下的时间堆栈的线程。 对于此示例中，我们要筛选此视图进一步通过仅包括与我们的包的模块名称和启动线程的堆栈。

1. 设置**GroupPats**为空文本，以便删除默认情况下添加任何分组。
2. 设置**IncPats**包含的程序集名称和线程启动除了现有的进程筛选器的部分。 在这种情况下，它应为**devenv;启动线程;MakeVsSlowExtension**。

现在，视图仅显示与扩展相关的程序集与关联的成本。 在此视图中，任何时候列入**Inc （非独占成本）** 启动线程的列与我们经过筛选的扩展，并将会影响启动。

一些有趣的调用上面的示例将为堆栈：

1. IO 使用`System.IO`类：这些框架中的非独占成本可能不是在跟踪中过于昂贵，尽管它们是可能会造成问题，由于文件 IO 速度将不同计算机之间。

   ![系统 io 帧](media/perfview-system-io-frames.png)

2. 阻止等待其他异步工作的调用：在这种情况下，非独占时间表示主线程阻塞在异步工作的完成时间。

   ![阻止调用框架](media/perfview-blocking-call-frames.png)

可以将有助于确定影响在跟踪中的其他视图之一**图像负载堆栈**。 您可以应用相同的筛选器应用于**线程时堆栈**查看并找出所有程序集加载，因为将自动加载的包执行的代码。

若要为每个其他程序集将涉及额外的磁盘 I/O，从而可以显著上较慢的计算机的启动变慢，包初始化例程中加载的程序集的数量降至最低至关重要。

## <a name="summary"></a>总结

启动 Visual Studio 已我们不断获得的反馈的领域之一。 我们如上文所述的目标是为所有用户都以一致方式启动而不考虑组件和扩展已安装体验。 我们想要使用扩展所有者，以帮助他们帮助我们实现这一目标。 上述指南应有助于了解扩展影响在启动和既无需自动加载或加载它以异步方式来对用户工作效率的影响降至最低。
