---
title: 如何：提供异步视觉工作室服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65362e465beec5465903083beca069104a48166b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710757"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>如何：提供异步视觉工作室服务
如果要在不阻塞 UI 线程的情况下获取服务，则应创建异步服务并将包加载到后台线程上。 为此，<xref:Microsoft.VisualStudio.Shell.AsyncPackage>可以使用 而不是 ，<xref:Microsoft.VisualStudio.Shell.Package>并使用异步包的特殊异步方法添加服务。

 有关提供同步 Visual Studio 服务的信息，请参阅[如何：提供服务](../extensibility/how-to-provide-a-service.md)。

## <a name="implement-an-asynchronous-service"></a>实现异步服务

1. 创建一个 VSIX 项目 （**文件** > **新项目** > **Project** > **可视化 C#** > **扩展性** > **VSIX 项目**）。 命名项目**TestAsync**。

2. 向项目添加 VS 包。 在**解决方案资源管理器**中选择项目节点，然后单击 **"添加新** > **项目** > **Visual C# 项目** > **扩展可视化** > **工作室包**"。 TestAsyncPackage.cs命名此*文件。*

3. 在*TestAsyncPackage.cs*中，将包更改为`AsyncPackage`从`Package`继承，而不是 ：

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. 要实现服务，您需要创建三种类型：

    - 标识服务的接口。 其中许多接口为空，也就是说，它们没有方法，因为它们仅用于查询服务。

    - 描述服务接口的接口。 此接口包括要实现的方法。

    - 实现服务和服务接口的类。

5. 下面的示例显示了三种类型的基本实现。 服务类的构造函数必须设置服务提供者。 在此示例中，我们将将服务添加到包代码文件中。

6. 将以下使用指令添加到包文件中：

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 下面是异步服务实现。 请注意，您需要设置异步服务提供者，而不是构造函数中的同步服务提供者：

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
 要注册服务，请将<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>添加到提供该服务的包。 与注册同步服务不同，您必须确保包和服务都支持异步加载：

- 您必须将 **"允许后台加载 = 真实**"字段<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>添加到 ，以确保包可以异步初始化，有关包注册属性的详细信息，请参阅[注册和取消注册 VSPackage。](../extensibility/registering-and-unregistering-vspackages.md)

- 您必须将**IsAsync 可查询 = 真实**字段<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>添加到 中，以确保服务实例可以异步初始化。

  下面是`AsyncPackage`具有异步服务注册的 示例：

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>添加服务

1. 在*TestAsyncPackage.cs*中，`Initialize()`删除 方法并`InitializeAsync()`重写 该方法。 添加服务，并添加回调方法来创建服务。 下面是异步初始化器添加服务的示例：

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    要使此服务在此包之外可见，将升级标志值设置为*true*作为最后一个参数：`this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. 添加对*微软的引用.VisualStudio.shell.Interop.14.0.DesignTime.dll*.

3. 将回调方法实现为创建和返回服务的异步方法。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>使用服务
 现在，您可以获取服务并使用其方法。

1. 我们将在初始化程序中显示这一点，但您可以在任何要使用该服务的地方获取服务。

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

     不要忘记更改为`userpath`文件名和在计算机上有意义的路径！

2. 生成并运行代码。 当 Visual Studio 的实验实例出现时，打开解决方案。 这将导致 自动`AsyncPackage`加载。 初始化程序运行后，应在指定的位置找到文件。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>在命令处理程序中使用异步服务
 下面是如何在菜单命令中使用异步服务的示例。 您可以使用此处显示的过程在其他非异步方法中使用服务。

1. 向项目添加菜单命令。 （在**解决方案资源管理器**中，选择项目节点，右键单击，然后选择 **"** > **添加新项目** > **扩展性** > **自定义命令**."TestAsyncCommand.cs命名*命令文件。*

2. 自定义命令模板将`Initialize()`方法重新添加到*TestAsyncPackage.cs*文件，以便初始化该命令。 在`Initialize()`方法中，复制初始化命令的行。 它看起来应该如下所示：

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     将此行移动到*AsyncPackageForService.cs*文件中`InitializeAsync()`的方法。 由于这是异步初始化中，因此在使用<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>初始化命令之前，必须切换到主线程。 它现在应如下所示：

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

4. 在*TestAsyncCommand.cs*文件中，查找方法`MenuItemCallback()`。 删除方法的正文。

5. 添加 using 指令：

    ```csharp
    using System.IO;
    ```

6. 添加名为 的`UseTextWriterAsync()`异步方法，该方法获取服务并使用其方法：

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

7. 从`MenuItemCallback()`方法调用此方法：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. 生成解决方案并启动调试。 当 Visual Studio 的实验实例出现时，转到 **"工具"** 菜单并查找 **"调用测试 Async命令"** 菜单项。 单击它时，TextWriterService 会写入您指定的文件。 （您无需打开解决方案，因为调用该命令也会导致加载包。

## <a name="see-also"></a>请参阅
- [使用和提供服务](../extensibility/using-and-providing-services.md)
