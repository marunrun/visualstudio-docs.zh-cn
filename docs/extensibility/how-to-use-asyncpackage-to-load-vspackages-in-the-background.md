---
title: 如何：使用 AsyncPackage 在后台加载 Vspackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: 7727d53c84ab876fe6616c8ec5d438033216481e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905599"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>如何：使用 AsyncPackage 在后台加载 Vspackage
加载和初始化 VS 包可能会导致磁盘 i/o。 如果 UI 线程上发生此类 i/o，则可能导致响应能力问题。 为了解决此情况，Visual Studio 2015 引入了在 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 后台线程上启用包加载的类。

## <a name="create-an-asyncpackage"></a>创建 AsyncPackage
 首先，可以创建一个 VSIX 项目（**文件**"  >  **新建**  >  **项目**" "  >  **Visual c #**  >  **扩展性**  >  **VSIX 项目**"）并将 VSPackage 添加到该项目（右键单击该项目，然后**添加**  >  **新**的 "  >  **c # 项目**  >  **扩展性**"  >  **Visual Studio 包**）。 然后，可以创建服务并将这些服务添加到包。

1. 从派生包 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 。

2. 如果提供的服务的查询可能会导致包加载：

    若要向 Visual Studio 指示你的包对于后台加载是安全的并且要选择加入此行为， <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 应在属性构造函数中将**AllowsBackgroundLoading**属性设置为 true。

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    若要指示 Visual Studio 可以安全地在后台线程上实例化服务，应 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A> 在构造函数中将属性设置为 true <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 。

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. 如果是通过 UI 上下文加载，则应将**PackageAutoLoadFlags.BackgroundLoad** <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 或值（0x2）指定为作为包自动加载条目的值写入的标志。

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. 如果有异步初始化工作要做，应重写 <xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A> 。 删除 `Initialize()` VSIX 模板提供的方法。 （ `Initialize()` **AsyncPackage**中的方法是密封的）。 可以使用任何 <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> 方法将异步服务添加到包。

    注意：若要调用 `base.InitializeAsync()` ，可以将源代码更改为：

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. 你必须小心，不要从异步初始化代码（在**app.mobileservice.synccontext.initializeasync**中）发出 Rpc （远程过程调用）。 直接或间接调用时，可能会出现这些情况 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 。  需要同步加载时，UI 线程将使用阻止 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> 。 默认阻塞模型将禁用 Rpc。 这意味着，如果你尝试从异步任务使用 RPC，则如果 UI 线程本身正在等待包加载，则会死锁。 一般的替代方法是使用**可加入任务工厂** <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 或其他不使用 RPC 的机制等，将代码封送到 UI 线程（如果需要）。  不要使用**ThreadHelper**或通常阻止正在等待访问 UI 线程的调用线程。

    注意：应避免在方法中使用**GetService**或**QueryService** `InitializeAsync` 。 如果需要使用这些参数，则需要先切换到 UI 线程。 替代方法是在 <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> **AsyncPackage**中使用（通过将其强制转换为 <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider> ）。

   C #：创建 AsyncPackage：

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

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>将现有 VSPackage 转换为 AsyncPackage
 大部分工作与创建新的**AsyncPackage**相同。 按照上面的步骤1到步骤5进行操作。 还需要对以下建议进行额外的小心：

1. 请记住删除 `Initialize` 包中的替代。

2. 避免死锁：代码中可能存在隐藏的 Rpc。 这是在后台线程上发生的。 请确保如果要进行 RPC （例如， **GetService**），则需要（1）切换到主线程，或（2）使用 API 的异步版本（如**getserviceasyn**）。

3. 不要过于频繁地在线程之间切换。 尝试本地化后台线程中可能发生的工作以减少加载时间。

## <a name="querying-services-from-asyncpackage"></a>从 AsyncPackage 查询服务
 **AsyncPackage**可能会（也可能不）以异步方式加载，具体取决于调用方。 例如，

- 如果调用方调用了**GetService**或**QueryService** （两个同步 api）或

- 如果调用方调用了**IVsShell：： LoadPackage** （或**IVsShell5：： LoadPackageWithContext**）或

- 负载由 UI 上下文触发，但未指定 UI 上下文机制可以异步加载

  然后，包将同步加载。

  你的包在其异步初始化阶段仍有机会在 UI 线程中执行工作，不过，UI 线程将在该工作完成时被阻止。 如果调用方使用**IAsyncServiceProvider**异步查询你的服务，则你的负载和初始化将以异步方式执行，前提是它们不会在生成的任务对象上立即阻止。

  C #：如何以异步方式查询服务：

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
