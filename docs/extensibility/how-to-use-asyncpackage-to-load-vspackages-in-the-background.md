---
title: 如何：使用异步包在后台加载 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: 77690a1947f82f97c4aa12809a80ea61335d216d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710620"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>如何：使用异步包在后台加载 VS 包
加载和初始化 VS 包可能会导致磁盘 I/O。 如果此类 I/O 发生在 UI 线程上，则可能导致响应问题。 为了解决这个问题，Visual Studio 2015<xref:Microsoft.VisualStudio.Shell.AsyncPackage>引入了允许在后台线程上加载包的类。

## <a name="create-an-asyncpackage"></a>创建异步包
 您可以开始创建一个 VSIX 项目 （**Project** > **文件** > **新项目** > **可视化 C_** > 扩展**VSIX** > **项目**） 和向项目添加 VS 包 （右键单击项目并**添加新** > **项目** > **C# 项** > **扩展可视化** > **工作室包**）。 然后，您可以创建服务并将这些服务添加到包中。

1. 从<xref:Microsoft.VisualStudio.Shell.AsyncPackage>派生包。

2. 如果您提供的服务的查询可能会导致加载您的包：

    要向 Visual Studio 指示您的包对后台加载是安全的，并选择加入此行为，<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>您应该在属性构造函数中将 **"允许后台加载**"属性设置为 true。

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    要向 Visual Studio 指示在后台线程上实例化服务是安全的，应在构造函数中<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A><xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>将属性设置为 true。

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. 如果通过 UI 上下文加载，则应将<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>或 值 （0x2） 的 **"包自动加载Flags"** 指定到作为包自动加载条目的值编写的标志中的后台加载。

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. 如果要执行异步初始化工作，则应重写<xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A>。 删除`Initialize()`VSIX 模板提供的方法。 （`Initialize()`**异步包**中的方法是密封的）。 可以使用任何<xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A>方法向包添加异步服务。

    注： 要`base.InitializeAsync()`调用 ，您可以将源代码更改为：

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. 您必须注意不要从异步初始化代码（**初始化 Async**中）进行 RPC（远程过程调用）。 当您直接或间接调用<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>时，可能会发生这些情况。  当需要同步加载时，UI 线程将使用<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>阻止。 默认阻止模型禁用 RPC。 这意味着，如果您尝试使用来自异步任务的 RPC，如果 UI 线程本身正在等待加载包，则将死锁。 通常的替代方法是，如果需要，请使用可**加入任务工厂**<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>或其他不使用 RPC 的机制将代码封送到 UI 线程。  不要使用**ThreadHelper.generic.Invoke 或**通常阻止等待到达 UI 线程的调用线程。

    注意：您应该避免在方法`InitializeAsync`中使用**获取服务**或**查询服务**。 如果必须使用这些线程，则需要首先切换到 UI 线程。 另一种方法是从<xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A>**Async 包**中使用（将其强制转换到<xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider>。）

   C#： 创建异步包：

```csharp
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]
public sealed class TestPackage : AsyncPackage
{
    protected override Task InitializeAsync(System.Threading.CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(SMyTestService), CreateService, true);
        return Task.FromResult<object>(null);
    }
}
```

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>将现有 VS 包转换为异步包
 大多数工作与创建新的**Async包**相同。 按照上面的步骤 1 到 5。 您还需要格外小心以下建议：

1. 请记住删除包中的`Initialize`重写。

2. 避免死锁：代码中可能有隐藏的 RPC。 现在发生在后台线程上。 请确保，如果要进行 RPC（例如 **，GetService），** 则需要 （1） 切换到主线程，或者 （2） 如果存在 API 的异步版本（例如 **，GetServiceAsync）。**

3. 请勿在线程之间切换过于频繁。 尝试本地化在后台线程中可能发生的工作，以减少加载时间。

## <a name="querying-services-from-asyncpackage"></a>从异步包查询服务
 **Async 包**可能加载，也可能不异步加载，具体取决于调用方。 例如，

- 如果呼叫者呼叫**获取服务**或**查询服务**（同时使用同步 API）或

- 如果调用方呼叫**IVsShell：加载包**（或**IVsShell5：：loadPackage 与上下文**） 或

- 负载由 UI 上下文触发，但您没有指定 UI 上下文机制可以异步加载您

  然后，您的包将同步加载。

  包仍然有机会（处于异步初始化阶段）从 UI 线程执行工作，尽管 UI 线程将被阻止完成该工作。 如果调用方使用**IAsyncServiceProvider**对服务进行异步查询，则加载和初始化将以异步方式完成，前提是它们不会立即阻止生成的任务对象。

  C#：如何异步查询服务：

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
