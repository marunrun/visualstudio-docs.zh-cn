---
title: 如何：提供异步 Visual Studio 服务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad178bf93e49c3d695c1ebd0a5d4f6b151175953
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905736"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>如何：提供异步 Visual Studio 服务
如果要在不阻止 UI 线程的情况下获取服务，则应创建一个异步服务，并在后台线程上加载该包。 出于此目的，你可以使用 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 而不是 <xref:Microsoft.VisualStudio.Shell.Package> ，并使用异步包的特殊异步方法添加服务。

 有关提供同步 Visual Studio 服务的信息，请参阅[如何：提供服务](../extensibility/how-to-provide-a-service.md)。

## <a name="implement-an-asynchronous-service"></a>实现异步服务

1. 创建 VSIX 项目（**文件**"  >  **新建**  >  **项目**" "  >  **Visual c #**  >  **所在**  >  **VSIX 项目**"）。 将项目命名为**TestAsync**。

2. 将 VSPackage 添加到项目。 在**解决方案资源管理器**中选择项目节点，然后单击 "**添加**  >  **新项**" "  >  **visual c # 项目**  >  **扩展性**" "  >  **visual Studio 包**"。 将此文件命名为*TestAsyncPackage.cs*。

3. 在*TestAsyncPackage.cs*中，将包更改为继承自 `AsyncPackage` 而不是 `Package` ：

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. 若要实现服务，需要创建以下三种类型：

    - 标识该服务的接口。 其中的许多接口都是空的，也就是说，它们没有用于查询服务的方法。

    - 描述服务接口的接口。 此接口包含要实现的方法。

    - 一个实现服务和服务接口的类。

5. 下面的示例演示了三种类型的一个非常基本的实现。 服务类的构造函数必须设置服务提供程序。 在此示例中，我们只将该服务添加到包代码文件中。

6. 向包文件添加以下 using 指令：

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 下面是异步服务实现。 请注意，需要在构造函数中设置异步服务提供程序，而不是同步服务提供程序：

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
 若要注册服务，请将添加 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 到提供该服务的包中。 不同于注册同步服务，必须确保包和服务支持异步加载：

- 必须将**AllowsBackgroundLoading = true**字段添加到 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 以确保可以异步初始化包有关 PackageRegistrationAttribute 的详细信息，请参阅[注册和注销 vspackage](../extensibility/registering-and-unregistering-vspackages.md)。

- 必须将**IsAsyncQueryable = true**字段添加到中， <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 以确保可以异步初始化服务实例。

  下面是一个 `AsyncPackage` 带有异步服务注册的示例：

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>添加服务

1. 在*TestAsyncPackage.cs*中，删除 `Initialize()` 方法并重写 `InitializeAsync()` 方法。 添加服务，并添加用于创建服务的回调方法。 下面是异步初始值设定项添加服务的示例：

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    若要使此服务在此包外可见，请将 "升级标志" 值设置为 " *true* " 作为最后一个参数：`this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. 添加对*Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll*的引用。

3. 实现回调方法，作为创建和返回服务的异步方法。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>使用服务
 现在，可以获取服务并使用其方法。

1. 在初始值设定项中将显示这种情况，但你可以在想要使用该服务的任何位置获取该服务。

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

     不要忘记改 `userpath` 为在计算机上有意义的文件名和路径！

2. 生成并运行代码。 出现 Visual Studio 的实验实例时，打开解决方案。 这将导致 `AsyncPackage` autoload。 初始值设定项运行后，应在指定的位置找到文件。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>在命令处理程序中使用异步服务
 下面是如何在菜单命令中使用异步服务的示例。 您可以使用此处所示的过程，在其他非异步方法中使用该服务。

1. 向项目中添加一个菜单命令。 （在 "**解决方案资源管理器**中，选择" 项目 "节点，右键单击，然后选择"**添加**  >  "**新建项**  > **扩展性**  > **自定义命令**。）将命令文件命名为*TestAsyncCommand.cs*。

2. 自定义命令模板会将方法重新添加 `Initialize()` 到*TestAsyncPackage.cs*文件，以便初始化命令。 在 `Initialize()` 方法中，复制用于初始化命令的行。 应如下所示：

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     将此行移到 `InitializeAsync()` *AsyncPackageForService.cs*文件中的方法。 由于这是异步初始化，因此在使用初始化命令之前，必须切换到主线程 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 。 它现在应如下所示：

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

3. 删除 `Initialize()` 方法。

4. 在*TestAsyncCommand.cs*文件中，找到 `MenuItemCallback()` 方法。 删除方法的正文。

5. 添加 using 指令：

    ```csharp
    using System.IO;
    ```

6. 添加一个名为的异步方法 `UseTextWriterAsync()` ，该方法可获取服务并使用其方法：

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

7. 从方法中调用此方法 `MenuItemCallback()` ：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. 生成解决方案并启动调试。 显示 Visual Studio 的实验实例后，请切换到 "**工具**" 菜单，然后查找 "**调用 TestAsyncCommand** " 菜单项。 单击该文件时，TextWriterService 将写入指定的文件。 （无需打开解决方案，因为调用命令也会导致包加载。）

## <a name="see-also"></a>另请参阅
- [使用并提供服务](../extensibility/using-and-providing-services.md)
