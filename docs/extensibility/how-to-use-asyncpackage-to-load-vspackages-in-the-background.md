---
title: 如何：使用 AsyncPackage 加载 Vspackage 背景 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: madskristensen
ms.author: madsk
ms.workload:
- vssdk
ms.openlocfilehash: 64514a6d43d580fbda142dfa65bb3a2d384dff4e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324780"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>如何：使用 AsyncPackage 在后台加载 Vspackage
加载和初始化 VS 包可能会导致磁盘 I/O。 如果此类 I/O 在 UI 线程上发生的情况，它会导致响应能力问题。 若要解决此问题，Visual Studio 2015 引入了<xref:Microsoft.VisualStudio.Shell.AsyncPackage>类，使包加载在后台线程上的。

## <a name="create-an-asyncpackage"></a>创建 AsyncPackage
 可以首先创建一个 VSIX 项目 (**文件** > **新建** > **项目** > **Visual C#**  > **扩展性** > **VSIX 项目**) 并将 VSPackage 添加到项目 (右键单击该项目并**添加** > **新项** >   **C#项** > **扩展性** >  **Visual Studio 包**)。 然后，可以创建你的服务，并将这些服务添加到您的包。

1. 派生从包<xref:Microsoft.VisualStudio.Shell.AsyncPackage>。

2. 如果你要提供的服务的查询可能会导致包加载：

    指示 Visual studio 包是安全的后台加载并用于选择加入此行为，你<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>应设置**AllowsBackgroundLoading**属性设为 true 的特性构造函数中。

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    若要指示 Visual Studio，则可以安全地实例化您的服务在后台线程上，应设置<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A>属性设为 true 中<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>构造函数。

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. 如果要通过 UI 上下文加载，则应指定**PackageAutoLoadFlags.BackgroundLoad**为<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>或作为包的自动加载项的值写入到标志的值 (0x2)。

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. 如果异步初始化可执行的操作，应重写<xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A>。 删除`Initialize()`VSIX 模板提供的方法。 (`Initialize()`中的方法**AsyncPackage**都密封的)。 可以使用任一<xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A>方法将异步服务添加到您的包。

    注意：若要调用`base.InitializeAsync()`，可以更改为你的源代码：

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. 必须小心以免使 Rpc （远程过程调用） 通过异步初始化代码 (在**InitializeAsync**)。 可以在调用时<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>直接或间接。  当同步加载是必需的时 UI 线程将会阻止使用<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>。 默认阻止模型禁用 Rpc。 这意味着，如果您尝试使用 RPC 从异步任务，您将发生死锁，如果 UI 线程正在等待加载对包本身。 常规的替代方法是封送到 UI 线程代码，如果需要使用类似**可加入任务工厂**的<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>或不使用 RPC 的其他一些机制。  不要使用**ThreadHelper.Generic.Invoke**或通常阻止调用线程正在等待获取对 UI 线程。

    注意：应避免使用**GetService**或**QueryService**在你`InitializeAsync`方法。 如果您必须使用这些，您需要先切换到 UI 线程。 替代方法是使用<xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A>从你**AsyncPackage** (通过它强制转换为<xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider>。)

   C#：创建 AsyncPackage:

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

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>将现有的 VSPackage 转换为 AsyncPackage
 大部分工作是创建一个新相同**AsyncPackage**。 执行步骤 1 至 5 更高版本。 此外需要额外的要小心，使用以下建议：

1. 请记住删除`Initialize`必须在包中的重写。

2. 避免死锁：可能有隐藏在代码中的 Rpc。 现在发生在后台线程上。 请确保，如果要进行 RPC (例如， **GetService**)，需要转到主线程 (1) 或 （2） 使用一个 API 的异步版本存在 (例如， **GetServiceAsync**).

3. 请勿过于频繁地在线程之间切换。 尝试将本地化可以发生在后台线程来减少加载时间的工作。

## <a name="querying-services-from-asyncpackage"></a>查询从 AsyncPackage 服务
 **AsyncPackage**可能或可能不会加载以异步方式具体取决于调用方。 例如，

- 如果调用方调用**GetService**或**QueryService** (这两个同步 Api) 或

- 如果调用方调用**IVsShell::LoadPackage** (或**IVsShell5::LoadPackageWithContext**) 或

- 负载触发 UI 上下文，但未指定的 UI 上下文机制可以以异步方式加载您

  然后，您的包将以同步方式加载。

  包仍有机会 （在异步初始化阶段） 来完成工作出 UI 线程，尽管 UI 线程将阻止该工作完成。 如果调用方将使用**IAsyncServiceProvider**异步查询你的服务，然后加载和初始化将完成异步假定它们不立即阻止生成的任务对象上。

  C#：如何以异步方式查询服务：

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
