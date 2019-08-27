---
title: 如何：提供异步服务 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0c58b0be10bf10a21b783a48d52806bf769381ee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204100"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>如何：提供异步 Visual Studio 服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你想要获取服务而不会阻塞 UI 线程，您应创建异步服务，并加载在后台线程上的包。 可以使用为此目的<xref:Microsoft.VisualStudio.Shell.AsyncPackage>而非<xref:Microsoft.VisualStudio.Shell.Package>，使用异步包的特殊异步方法中添加服务

 有关提供同步 Visual Studio 服务的信息，请参阅[如何：提供的服务](../extensibility/how-to-provide-a-service.md)。

## <a name="implementing-an-asynchronous-service"></a>实现异步服务

1. 创建一个 VSIX 项目 (**文件 / 新建 / 项目 / Visual C# / 建议 / VSIX 项目**)。 将项目命名**TestAsync**。

2. 将 VSPackage 添加到项目。 选择中的项目节点**解决方案资源管理器**然后单击**添加 / 新建项 / Visual C# 项 / 可扩展性 / Visual Studio 包**。 此文件命名**TestAsyncPackage.cs**。

3. 在 TestAsyncPackage.cs，来更改要继承 AsyncPackage 而不是包的包：

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. 若要实现的服务，需要创建三种类型：

    - 一个描述该服务的接口。 许多这些接口是空的也就是说，它们有没有方法。

    - 一个描述服务接口的接口。 此接口包括要实现的方法。

    - 实现服务和服务接口的类。

5. 下面的示例显示了三种类型的非常基本的实现。 服务类的构造函数必须设置的服务提供程序。 在此示例中我们将只是将服务添加到包的代码文件。

6. 将以下代码添加到包文件 using 语句：

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    ```

7. 下面是异步的服务实现。 请注意，您需要在构造函数中设置的异步服务提供程序而不是同步服务提供程序：

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
 若要注册一个服务，将添加<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>到提供的服务包。 有两个区别注册同步服务：

- 如果要自动加载包，必须添加<xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags>BackgroundLoad 值的属性。 有关自动加载 Vspackage 的详细信息，请参阅[加载 Vspackage](../extensibility/loading-vspackages.md)。

- 必须添加**AllowsBackgroundLoading = true**字段<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>。 有关 PackageRegistrationAttribute 详细信息，请参阅[注册和注销 Vspackage](../extensibility/registering-and-unregistering-vspackages.md)。

  下面是使用异步服务注册 AsyncPackage 的示例::

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="adding-a-service"></a>添加服务

1. 在 TestAsyncPackage.cs，删除`Initialize()`方法，并替代`InitializeAsync()`方法。 添加服务，并添加一个用于创建服务的回调方法。 下面是添加服务的异步初始值设定项的示例：

    ```
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(STextWriterService), CreateService);

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

2. 添加对 Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll 的引用。

3. 为异步方法，创建并返回该服务实现的回调方法。

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
 现在，您可以获取该服务，使用它的方法。

1. 我们将介绍这在初始值设定项，但您可以获取的服务任意位置你想要使用服务。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(STextWriterService), CreateService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;

        await writer.WriteLineAsync(<userpath>), "this is a test");

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

     不要忘记更改 *\<userpath >* 到的文件名和路径在计算机上有意义的 ！

2. 生成并运行代码。 Visual Studio 的实验实例出现时，打开的解决方案。 这会导致自动加载 AsyncPackage。 初始值设定项开始运行后，您应查找中指定的位置的文件。

## <a name="using-an-asynchronous-service-in-a-command-handler"></a>在命令处理程序中使用异步服务
 下面是如何使用异步服务中的菜单命令的示例。 可以使用此处显示要在其他非异步方法中使用该服务的过程。

1. 将菜单命令添加到你的项目。 (在**解决方案资源管理器**，选择项目节点，右键单击，并选择**添加 / 新项 / 扩展 / 自定义命令**。)命令文件命名为**TestAsyncCommand.cs。**

2. 自定义命令模板重新添加`Initialize()`TestAsyncPackage.cs 文件才能初始化该命令的方法。 在 initialize （） 方法中，将复制该命令的行。 应如下所示：

    ```
    TestAsyncCommand.Initialize(this);
    ```

     将移动到此行`InitializeAsync()`AsyncPackageForService.cs 文件中的方法。 由于这是异步初始化中，必须切换到主线程初始化命令使用之前<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>。 它现在应如下所示：

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

3. 删除`Initialize()`方法。

4. 在 TestAsyncCommand.cs 文件中，找到`MenuItemCallback()`方法。 删除方法的主体。

5. 添加 using 语句：

    ```
    using System.IO;
    ```

6. 添加名为的异步方法`GetAsyncService()`，其获取的服务，并使用其方法：

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

7. 调用此方法从`MenuItemCallback()`方法：

    ```
    private void MenuItemCallback(object sender, EventArgs e)
    {
        GetAsyncService();
    }

    ```

8. 生成解决方案并启动调试。 Visual Studio 的实验实例出现时，请转到**工具**菜单，并寻找**调用 TestAsyncCommand**菜单项。 当您单击它时，TextWriterService 将写入到指定的文件。 （您不需要打开的解决方案，因为调用该命令还会导致要加载的包。）

## <a name="see-also"></a>请参阅
 [使用并提供服务](../extensibility/using-and-providing-services.md)
