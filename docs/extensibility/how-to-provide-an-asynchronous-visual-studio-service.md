---
title: 如何：提供异步 Visual Studio 服务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9628a3e352d2662fe150ec7ef4cda7c79a2fdffa
ms.sourcegitcommit: 01c3c9dcade5d913bde2c7efa8c931a7b04e6cd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365681"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>如何：提供异步 Visual Studio 服务
如果你想要获取服务而不会阻塞 UI 线程，您应创建异步服务，并加载在后台线程上的包。 可以使用为此目的<xref:Microsoft.VisualStudio.Shell.AsyncPackage>而非<xref:Microsoft.VisualStudio.Shell.Package>，使用异步包的特殊异步方法中添加服务。

 有关提供同步 Visual Studio 服务的信息，请参阅[如何：提供的服务](../extensibility/how-to-provide-a-service.md)。

## <a name="implement-an-asynchronous-service"></a>实现异步服务

1. 创建一个 VSIX 项目 (**文件** > **新建** > **项目** > **Visual C#**  > **建议** > **VSIX 项目**)。 将项目命名**TestAsync**。

2. 将 VSPackage 添加到项目。 选择中的项目节点**解决方案资源管理器**然后单击**添加** > **新项** > **Visual C# 项**  > **扩展性** > **Visual Studio 包**。 此文件命名*TestAsyncPackage.cs*。

3. 在中*TestAsyncPackage.cs*，更改要继承的程序包`AsyncPackage`而非`Package`:

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. 若要实现的服务，需要创建三种类型：

    - 一个标识该服务的接口。 许多这些接口是空的因为它们仅用于查询服务，即它们有没有方法。

    - 一个描述服务接口的接口。 此接口包括要实现的方法。

    - 实现服务和服务接口的类。

5. 下面的示例显示了三种类型的非常基本的实现。 服务类的构造函数必须设置的服务提供程序。 在此示例中我们将只是将服务添加到包的代码文件。

6. 将以下代码添加到包文件 using 语句：

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 下面是异步的服务实现。 请注意，您需要在构造函数中设置的异步服务提供程序而不是同步服务提供程序：

    ```csharp
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private IAsyncServiceProvider asyncServiceProvider;

        public TextWriterService(IAsyncServiceProvider provider)
        {
            // constructor should only be used for simple initialization
            // any usage of Visual Studio service, expensive background operations should happen in the
            // asynchronous InitializeAsync method for best performance
            asyncServiceProvider = provider;
        }

        public async Task InitializeAsync(CancellationToken cancellationToken)
        {
            await TaskScheduler.Default;
            // do background operations that involve IO or other async methods

            await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
            // query Visual Studio services on main thread unless they are documented as free threaded explicitly.
            // The reason for this is the final cast to service interface (such as IVsShell) may involve COM operations to add/release references.

            IVsShell vsShell = this.asyncServiceProvider.GetServiceAsync(typeof(SVsShell)) as IVsShell;
            // use Visual Studio services to continue initialization
        }

        public async Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
    }

    public interface STextWriterService
    {
    }

    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
    }
    ```

## <a name="register-a-service"></a>注册服务
 若要注册一个服务，将添加<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>到提供的服务包。 不同于注册同步服务，你必须确保包和服务都支持异步加载：

- 必须添加**AllowsBackgroundLoading = true**字段<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>若要确保包可以以异步方式初始化 PackageRegistrationAttribute 有关详细信息，请参阅[注册和注销 Vspackage](../extensibility/registering-and-unregistering-vspackages.md)。

- 必须添加**IsAsyncQueryable = true**字段<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>以确保可以以异步方式初始化服务实例。

  下面是示例的`AsyncPackage`使用异步服务注册：

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>添加服务

1. 在中*TestAsyncPackage.cs*，删除`Initialize()`方法，并替代`InitializeAsync()`方法。 添加服务，并添加一个用于创建服务的回调方法。 下面是添加服务的异步初始值设定项的示例：

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```

2. 添加对的引用*Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll*。

3. 为异步方法，创建并返回该服务实现的回调方法。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>使用服务
 现在，您可以获取该服务，使用它的方法。

1. 我们将介绍这在初始值设定项，但您可以获取的服务任意位置你想要使用服务。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
    }

    ```

     不要忘记更改`userpath`到的文件名和路径在计算机上有意义的 ！

2. 生成并运行代码。 Visual Studio 的实验实例出现时，打开的解决方案。 这将导致`AsyncPackage`自动加载。 初始值设定项开始运行后，您应查找中指定的位置的文件。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>在命令处理程序中使用异步服务
 下面是如何使用异步服务中的菜单命令的示例。 可以使用此处显示要在其他非异步方法中使用该服务的过程。

1. 将菜单命令添加到你的项目。 (在**解决方案资源管理器**，选择项目节点，右键单击，并选择**添加** > **新项** >  **可扩展性** > **自定义命令**。)命令文件命名*TestAsyncCommand.cs*。

2. 自定义命令模板重新添加了`Initialize()`方法*TestAsyncPackage.cs*才能初始化该命令的文件。 在`Initialize()`方法中，将初始化命令行复制。 应如下所示：

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     将移动到此行`InitializeAsync()`中的方法*AsyncPackageForService.cs*文件。 由于这是异步初始化中，必须切换到主线程初始化命令使用之前<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>。 它现在应如下所示：

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");

        await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
        TestAsyncCommand.Initialize(this);
    }

    ```

3. 删除`Initialize()`方法。

4. 在中*TestAsyncCommand.cs*文件中，找到`MenuItemCallback()`方法。 删除方法的主体。

5. 添加 using 语句：

    ```csharp
    using System.IO;
    ```

6. 添加名为的异步方法`UseTextWriterAsync()`，其获取的服务，并使用其方法：

    ```csharp
    private async System.Threading.Tasks.Task UseTextWriterAsync()
    {
        // Query text writer service asynchronously to avoid a blocking call.
        ITextWriterService textService =
           await AsyncServiceProvider.GlobalProvider.GetServiceAsync(typeof(STextWriterService))
              as ITextWriterService;

        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
       }

    ```

7. 调用此方法从`MenuItemCallback()`方法：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. 生成解决方案并启动调试。 Visual Studio 的实验实例出现时，请转到**工具**菜单，并寻找**调用 TestAsyncCommand**菜单项。 当您单击它时，TextWriterService 将写入到指定的文件。 （您不需要打开的解决方案，因为调用该命令还会导致要加载的包。）

## <a name="see-also"></a>请参阅
- [使用和提供服务](../extensibility/using-and-providing-services.md)
