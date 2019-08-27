---
title: 如何：提供服务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a752e05e5a7c91e0e9f3d3c21f8542014a053245
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324970"
---
# <a name="how-to-provide-a-service"></a>如何：提供的服务
VSPackage 可以提供其他的 Vspackage 可以使用的服务。 若要提供服务，VSPackage 必须使用 Visual Studio 中注册该服务并将服务添加。

 <xref:Microsoft.VisualStudio.Shell.Package>类可实现<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>和<xref:System.ComponentModel.Design.IServiceContainer>。 <xref:System.ComponentModel.Design.IServiceContainer> 包含按需提供服务的回调方法。

 有关服务的详细信息，请参阅[服务 essentials](../extensibility/internals/service-essentials.md) 。

> [!NOTE]
> 当 VSPackage 即将卸载时，Visual Studio 等待，直到已传递为 VSPackage 提供的服务的所有请求。 它不允许对这些服务的新请求。 不应显式调用<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A>方法撤消时卸载服务。

## <a name="implement-a-service"></a>实现服务

1. 创建一个 VSIX 项目 (**文件** > **新建** > **项目** > **Visual C#**  > **扩展性** > **VSIX 项目**)。

2. 将 VSPackage 添加到项目。 选择中的项目节点**解决方案资源管理器**然后单击**添加** > **新项** > **Visual C# 项**  > **扩展性** > **Visual Studio 包**。

3. 若要实现的服务，需要创建三种类型：

   - 一个描述该服务的接口。 许多这些接口是空的也就是说，它们有没有方法。

   - 一个描述服务接口的接口。 此接口包括要实现的方法。

   - 实现服务和服务接口的类。

     下面的示例显示了三种类型的基本实现。 服务类的构造函数必须设置的服务提供程序。

   ```csharp
   public class MyService : SMyService, IMyService
   {
       private Microsoft.VisualStudio.OLE.Interop.IServiceProvider serviceProvider;
       private string myString;
       public MyService(Microsoft.VisualStudio.OLE.Interop.IServiceProvider sp)
       {
           Trace.WriteLine(
                  "Constructing a new instance of MyService");
           serviceProvider = sp;
       }
       public void Hello()
       {
           myString = "hello";
       }
       public string Goodbye()
       {
          return "goodbye";
       }
   }
   public interface SMyService
   {
   }
   public interface IMyService
   {
       void Hello();
       string Goodbye();
   }

   ```

### <a name="register-a-service"></a>注册服务

1. 若要注册一个服务，将添加<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>到 VSPackage 提供服务。 下面是一个示例：

    ```csharp
    [ProvideService(typeof(SMyService))]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [Guid(VSPackage1.PackageGuidString)]
    public sealed class VSPackage1 : Package
    {. . . }
    ```

     此属性注册`SMyService`使用 Visual Studio。

    > [!NOTE]
    > 若要注册一个服务来替换具有相同名称的另一个服务，请使用<xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute>。 请注意在允许的服务只有一个重写。

### <a name="add-a-service"></a>添加服务

1. VSPackage 初始值设定项中添加服务和一个用于创建服务的回调方法。 下面是要为进行的更改<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法：

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);
    . . .
    }
    ```

2. 实现回调方法，这应创建并返回该服务，或如果无法创建，则为 null。

    ```csharp
    private object CreateService(IServiceContainer container, Type serviceType)
    {
        if (typeof(SMyService) == serviceType)
            return new MyService(this);
        return null;
    }
    ```

    > [!NOTE]
    > Visual Studio 可以拒绝的请求提供服务。 它是如果另一个 VSPackage 已经提供了该服务。

3. 现在，您可以获取该服务，使用它的方法。 下面的示例显示了使用初始值设定项中的服务，但您可以获取的服务任意位置你想要使用服务。

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);

        MyService myService = (MyService) this.GetService(typeof(SMyService));
        myService.Hello();
        string helloString = myService.Goodbye();

        base.Initialize();
    }
    ```

     值`helloString`应为"Hello"。

## <a name="see-also"></a>请参阅
- [如何：获取服务](../extensibility/how-to-get-a-service.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [服务基础知识](../extensibility/internals/service-essentials.md)
