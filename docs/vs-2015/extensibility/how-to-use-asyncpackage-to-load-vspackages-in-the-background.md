---
title: 如何：使用 AsyncPackage 在后台加载 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
caps.latest.revision: 9
ms.author: gregvanl
ms.openlocfilehash: f59838913ed3f9bc6679336393f6db9181291e3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204022"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>如何：在后台使用 AsyncPackage 加载 Vspackage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

加载和初始化 VS 包可能会导致磁盘 i/o。 如果 UI 线程上发生此类 i/o，则可能导致响应能力问题。 为了解决此情况，Visual Studio 2015 引入了在  <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 后台线程上启用包加载的类。  
  
## <a name="creating-an-asyncpackage"></a>创建 AsyncPackage  
 首先，你可以创建一个 VSIX 项目 (**文件/新建/项目/Visual c #/扩展性/VSIX 项目**) 并向项目添加 VSPackage (右键单击项目，然后 **添加/新建项/c # 项/扩展性/Visual Studio 包**) 。 然后，可以创建服务并将这些服务添加到包。  
  
1. 从派生包 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 。  
  
2. 如果提供的服务的查询可能会导致包加载：  
  
    若要向 Visual Studio 指示你的包对于后台加载是安全的并且要选择加入此行为， <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 应在属性构造函数中将 **AllowsBackgroundLoading** 属性设置为 true。  
  
   ```csharp  
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]  
  
   ```  
  
    若要指示 Visual Studio 可以安全地在后台线程上实例化服务，应 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A> 在构造函数中将属性设置为 true <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 。  
  
   ```csharp  
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]  
  
   ```  
  
3. 如果是通过 UI 上下文加载，则应为指定 **PackageAutoLoadFlags** ，或者为指定 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 值 (0x2) 到作为包自动加载条目的值写入的标志。  
  
   ```csharp  
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]  
  
   ```  
  
4. 如果有异步初始化工作要做，应重写 <xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A> 。 删除 VSIX 模板提供的 **Initialize ( # B1 ** 方法。  (中的 **Initialize ( # B2 ** 方法 **是密封的) ** 。 可以使用任何 <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> 方法将异步服务添加到包。  
  
    注意：若要调用 **base.InitializeAsync ( # B1 **，可以将源代码更改为：  
  
   ```csharp  
   await base.InitializeAsync(cancellationToken, progress);  
   ```  
  
5. 您必须注意不要使 Rpc (从 **app.mobileservice.synccontext.initializeasync**) 中的异步初始化代码 (删除过程调用) 。 直接或间接调用时，可能会出现这些情况 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 。  需要同步加载时，UI 线程将使用阻止 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> 。 默认阻塞模型将禁用 Rpc。 这意味着，如果你尝试从异步任务使用 RPC，则如果 UI 线程本身正在等待包加载，则会死锁。 一般的替代方法是使用 **可加入任务工厂** <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 或其他不使用 RPC 的机制等，将代码封送到 UI 线程（如果需要）。  不要使用 **ThreadHelper** 或通常阻止正在等待访问 UI 线程的调用线程。  
  
    注意：应避免在**app.mobileservice.synccontext.initializeasync**方法中使用**GetService**或**QueryService** 。 如果需要使用这些参数，则需要先切换到 UI 线程。 替代方法是通过将 <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> **AsyncPackage** (强制转换为来使用 <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider> 。 )   
  
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
 大部分工作与创建新的 **AsyncPackage**相同。 你需要执行上面的步骤1到步骤5。 还需要对以下各项进行额外的警告：  
  
1. 请记住删除已在包中的 **初始化** 替代。  
  
2. 避免死锁：代码中可能存在隐藏的 Rpc，这些 Rpc 现在发生在后台线程上。 你需要确保在将 RPC (例如 **GetService**) 的情况下，你需要 (1) 切换到主线程，或 (2) 使用 API 的异步版本（如果存在 (例如 **getserviceasyn**) ）。  
  
3. 不要过于频繁地在线程之间切换。 尝试对后台线程中可能发生的工作进行本地化。 这会缩短加载时间。  
  
## <a name="querying-services-from-asyncpackage"></a>从 AsyncPackage 查询服务  
 **AsyncPackage**可能会（也可能不）以异步方式加载，具体取决于调用方。 例如，  
  
- 如果调用方调用了 **GetService** 或 **QueryService** (同步 api) 或  
  
- 如果调用方调用了 **IVsShell：： LoadPackage** (或 **IVsShell5：： LoadPackageWithContext**) 或  
  
- 负载由 UI 上下文触发，但未指定 UI 上下文机制可以异步加载  
  
  然后，包将同步加载。  
  
  请注意，你的包在其异步初始化阶段 (仍有机会) 在 UI 线程中执行工作，尽管 UI 线程将在该工作完成时被阻止。 如果调用方使用 **IAsyncServiceProvider** 异步查询你的服务，则你的负载和初始化将以异步方式执行，前提是它们不会在生成的任务对象上立即阻止。  
  
  C #：如何以异步方式查询服务：  
  
```csharp  
using Microsoft.VisualStudio.Shell;   
using Microsoft.VisualStudio.Shell.Interop;   
  
IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;   
IMyTestService testService = await ayncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;  
```
