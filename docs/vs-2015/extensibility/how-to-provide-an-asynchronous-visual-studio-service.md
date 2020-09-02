---
title: 如何：提供异步服务 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0c58b0be10bf10a21b783a48d52806bf769381ee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204100"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>如何：提供异步 Visual Studio 服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果要在不阻止 UI 线程的情况下获取服务，则应创建一个异步服务，并在后台线程上加载该包。 出于此目的，你可以使用 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> 而不是 <xref:Microsoft.VisualStudio.Shell.Package> ，并使用异步包的特殊异步方法添加服务。

 有关提供同步 Visual Studio 服务的信息，请参阅 [如何：提供服务](../extensibility/how-to-provide-a-service.md)。

## <a name="implementing-an-asynchronous-service"></a>实现异步服务

1. 创建 VSIX 项目 (**文件/新建/项目/Visual c #/所在/VSIX 项目**) 。 将项目命名为 **TestAsync**。

2. 将 VSPackage 添加到项目。 在 **解决方案资源管理器** 中选择项目节点，然后单击 " **添加/新建项"/"Visual c # 项"/"扩展性/visual Studio 包**"。 将此文件命名为 **TestAsyncPackage.cs**。

3. 在 TestAsyncPackage.cs 中，将包更改为继承自 AsyncPackage 而不是包：

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. 若要实现服务，需要创建以下三种类型：

    - 用于描述服务的接口。 其中的许多接口都是空的，也就是说，它们没有方法。

    - 描述服务接口的接口。 此接口包含要实现的方法。

    - 一个实现服务和服务接口的类。

5. 下面的示例演示了三种类型的一个非常基本的实现。 服务类的构造函数必须设置服务提供程序。 在此示例中，我们只将该服务添加到包代码文件中。

6. 向包文件添加以下 using 语句：

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    ```

7. 下面是异步服务实现。 请注意，需要在构造函数中设置异步服务提供程序，而不是同步服务提供程序：

    ```
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private Microsoft.VisualStudio.Shell.IAsyncServiceProvider serviceProvider;
        public TextWriterService(Microsoft.VisualStudio.Shell.IAsyncServiceProvider provider)
        {
            serviceProvider = provider;
        }
        public async System.Threading.Tasks.Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
        public TaskAwaiter GetAwaiter()
        {
            return new TaskAwaiter();
        }
    }
    public interface STextWriterService
    {
    }
    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
        TaskAwaiter GetAwaiter();
    }
    ```

## <a name="registering-a-service"></a>注册服务
 若要注册服务，请将添加 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> 到提供该服务的包中。 注册同步服务有两个不同之处：

- 如果对包自动加载，则必须将 <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> BackgroundLoad 值添加到属性。 有关自动加载 Vspackage 的详细信息，请参阅 [加载 vspackage](../extensibility/loading-vspackages.md)。

- 必须将 **AllowsBackgroundLoading = true** 字段添加到中 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 。 有关 PackageRegistrationAttribute 的详细信息，请参阅 [注册和注销 vspackage](../extensibility/registering-and-unregistering-vspackages.md)。

  下面是使用异步服务注册的 AsyncPackage 的示例：

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="adding-a-service"></a>添加服务

1. 在 TestAsyncPackage.cs 中，删除 `Initialize()` 方法并重写 `InitializeAsync()` 方法。 添加服务，并添加用于创建服务的回调方法。 下面是异步初始值设定项添加服务的示例：

    ```
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(STextWriterService), CreateService);

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

2. 添加对 Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll 的引用。

3. 实现回调方法，作为创建和返回服务的异步方法。

    ```csharp
    public async System.Threading.Tasks.Task<object> CreateService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        STextWriterService service = null;
        await System.Threading.Tasks.Task.Run(() => {
                    service = new TextWriterService(this);
             });

        return service;
    }

    ```

## <a name="using-a-service"></a>使用服务
 现在，可以获取服务并使用其方法。

1. 在初始值设定项中将显示这种情况，但你可以在想要使用该服务的任何位置获取该服务。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(STextWriterService), CreateService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;

        await writer.WriteLineAsync(<userpath>), "this is a test");

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

     不要忘记改 *\<userpath>* 为在计算机上有意义的文件名和路径！

2. 生成并运行代码。 出现 Visual Studio 的实验实例时，打开解决方案。 这会导致 AsyncPackage autoload。 初始值设定项运行后，应在指定的位置找到文件。

## <a name="using-an-asynchronous-service-in-a-command-handler"></a>在命令处理程序中使用异步服务
 下面是如何在菜单命令中使用异步服务的示例。 您可以使用此处所示的过程，在其他非异步方法中使用该服务。

1. 向项目中添加一个菜单命令。  (在 **解决方案资源管理器**中，选择 "项目" 节点，右键单击，然后选择 " **添加/新建项"/"扩展性"/"自定义命令**"。 ) 命名命令文件 **TestAsyncCommand.cs。**

2. 自定义命令模板会将方法重新添加 `Initialize()` 到 TestAsyncPackage.cs 文件，以便初始化命令。 在 Initialize ( # A1 方法中，复制用于初始化命令的行。 它应如下所示：

    ```
    TestAsyncCommand.Initialize(this);
    ```

     将此行移到 `InitializeAsync()` AsyncPackageForService.cs 文件中的方法。 由于这是异步初始化，因此在使用初始化命令之前，必须切换到主线程 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> 。 它现在应如下所示：

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        TestAsyncCommand.Initialize(this);

        this.AddService(typeof(STextWriterService), CreateService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;

        await writer.WriteLineAsync((<userpath>, "this is a test");

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

3. 删除 `Initialize()` 方法。

4. 在 TestAsyncCommand.cs 文件中，找到 `MenuItemCallback()` 方法。 删除方法的正文。

5. 添加 using 语句：

    ```
    using System.IO;
    ```

6. 添加一个名为的异步方法 `GetAsyncService()` ，该方法可获取服务并使用其方法：

    ```csharp
    private async System.Threading.Tasks.Task GetAsyncService()
    {
        ITextWriterService textService =
           this.ServiceProvider.GetService(typeof(STextWriterService))
              as ITextWriterService;
        // don’t forget to change <userpath> to a local path
        await writer.WriteLineAsync((<userpath>),"this is a test");
       }

    ```

7. 从方法中调用此方法 `MenuItemCallback()` ：

    ```
    private void MenuItemCallback(object sender, EventArgs e)
    {
        GetAsyncService();
    }

    ```

8. 生成解决方案并启动调试。 显示 Visual Studio 的实验实例后，请切换到 " **工具** " 菜单，然后查找 " **调用 TestAsyncCommand** " 菜单项。 单击该文件时，TextWriterService 将写入指定的文件。  (无需打开解决方案，因为调用命令也会导致加载包。 ) 

## <a name="see-also"></a>另请参阅
 [使用并提供服务](../extensibility/using-and-providing-services.md)
