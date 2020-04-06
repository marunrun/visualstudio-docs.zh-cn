---
title: 如何：提供服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 60cae5e8048a0234114e1f9e7d97728e26ee40f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710775"
---
# <a name="how-to-provide-a-service"></a>如何：提供服务
VS 包可以提供其他 VS 包可以使用的服务。 要提供服务，VSPackage 必须向 Visual Studio 注册服务并添加该服务。

 类<xref:Microsoft.VisualStudio.Shell.Package>实现 和<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider><xref:System.ComponentModel.Design.IServiceContainer>。 <xref:System.ComponentModel.Design.IServiceContainer>包含按需提供服务的回调方法。

 有关服务的详细信息，请参阅[服务要点](../extensibility/internals/service-essentials.md)。

> [!NOTE]
> 当 VSPackage 即将卸载时，Visual Studio 会等待，直到 VSPackage 提供的所有服务请求都已送达。 它不允许对这些服务进行新请求。 在卸载时，<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A>不应显式调用 方法以撤消服务。

## <a name="implement-a-service"></a>实现服务

1. 创建一个 VSIX 项目 （**文件** > **新项目** > **Project** > **可视化 C_** > **扩展 VSIX** > **项目**）。

2. 向项目添加 VS 包。 在**解决方案资源管理器**中选择项目节点，然后单击 **"添加新** > **项目** > **Visual C# 项目** > **扩展可视化** > **工作室包**"。

3. 要实现服务，您需要创建三种类型：

   - 描述服务的接口。 其中许多接口是空的，也就是说，它们没有方法。

   - 描述服务接口的接口。 此接口包括要实现的方法。

   - 实现服务和服务接口的类。

     下面的示例显示了三种类型的基本实现。 服务类的构造函数必须设置服务提供者。

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

1. 要注册服务，请将<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>添加到提供服务的 VSPackage。 以下是示例：

    ```csharp
    [ProvideService(typeof(SMyService))]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [Guid(VSPackage1.PackageGuidString)]
    public sealed class VSPackage1 : Package
    {. . . }
    ```

     此属性向`SMyService`Visual Studio 注册。

    > [!NOTE]
    > 要注册以相同名称替换另一个服务的服务，请使用 。 <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> 请注意，只允许一个服务重写。

### <a name="add-a-service"></a>添加服务

1. 在 VSPackage 初始化器中，添加服务并添加回调方法来创建服务。 下面是对<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法的更改：

    ```csharp
    protected override void Initialize()
    {
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);

        ((IServiceContainer)this).AddService(typeof(SMyService), callback);
    . . .
    }
    ```

2. 实现回调方法（应创建和返回服务）或 null（如果无法创建）。

    ```csharp
    private object CreateService(IServiceContainer container, Type serviceType)
    {
        if (typeof(SMyService) == serviceType)
            return new MyService(this);
        return null;
    }
    ```

    > [!NOTE]
    > Visual Studio 可以拒绝提供服务的请求。 如果另一个 VSPackage 已经提供服务，则这样做。

3. 现在，您可以获取服务并使用其方法。 下面的示例显示了在初始化器中使用服务，但您可以在要使用该服务的任何地方获取服务。

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

     的值`helloString`应该是"你好"。

## <a name="see-also"></a>请参阅
- [如何：获取服务](../extensibility/how-to-get-a-service.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [服务要点](../extensibility/internals/service-essentials.md)
