---
title: 如何：提供服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, providing
ms.assetid: 12bc1f12-47b1-44f6-b8db-862aa88d50d1
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 565a8a91797c826b6419dc5a8488d7d3baf9cddc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435913"
---
# <a name="how-to-provide-a-service"></a>如何：提供服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage 可以提供其他的 Vspackage 可以使用的服务。 若要提供服务，VSPackage 必须使用 Visual Studio 中注册该服务并将服务添加。  
  
 <xref:Microsoft.VisualStudio.Shell.Package>类可实现<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>和<xref:System.ComponentModel.Design.IServiceContainer>。 <xref:System.ComponentModel.Design.IServiceContainer> 包含按需提供服务的回调方法。  
  
 有关服务的详细信息，请参阅[服务基础知识](../extensibility/internals/service-essentials.md)。  
  
> [!NOTE]
> 当 VSPackage 即将卸载时，Visual Studio 等待，直到已传递为 VSPackage 提供的服务的所有请求。 它不允许对这些服务的新请求。 不应显式调用<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A>方法撤消时卸载服务。  
  
#### <a name="implementing-a-service"></a>实现服务  
  
1. 创建一个 VSIX 项目 (**文件 / 新建 / 项目 / Visual C# / 建议 / VSIX 项目**)。  
  
2. 将 VSPackage 添加到项目。 选择中的项目节点**解决方案资源管理器**然后单击**添加 / 新建项 / Visual C# 项 / 可扩展性 / Visual Studio 包**。  
  
3. 若要实现的服务，需要创建三种类型：  
  
   - 一个描述该服务的接口。 许多这些接口是空的也就是说，它们有没有方法。  
  
   - 一个描述服务接口的接口。 此接口包括要实现的方法。  
  
   - 实现服务和服务接口的类。  
  
     下面的示例显示了三种类型的非常基本的实现。 服务类的构造函数必须设置的服务提供程序。  
  
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
  
### <a name="registering-a-service"></a>注册服务  
  
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
  
### <a name="adding-a-service"></a>添加服务  
  
1. 1.  VSPackage 初始值设定项中添加服务和一个用于创建服务的回调方法。 下面是要为进行的更改<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法：  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
    . . .  
    }  
    ```  
  
2. 实现回调方法，这应创建并返回该服务，或如果无法创建，则为 null。  
  
    ```  
    private object CreateService(IServiceContainer container, Type serviceType)  
    {  
        if (typeof(SMyService) == serviceType)  
            return new SMyService(this);  
        return null;  
    }  
    ```  
  
    > [!NOTE]
    > Visual Studio 可以拒绝的请求提供服务。 它是如果另一个 VSPackage 已经提供了该服务。  
  
3. 现在，您可以获取该服务，使用它的方法。 我们将介绍这在初始值设定项，但您可以获取的服务任意位置你想要使用服务。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        ServiceCreatorCallback callback =new ServiceCreatorCallback(CreateService);  
  
        ((IServiceContainer)this).AddService(typeof(SMyService), callback);  
  
        MyService myService = (MyService) this.GetService(typeof(SMyService));  
        myService.Hello();  
        string helloString = myService.myString;  
  
        base.Initialize();  
    }  
    ```  
  
     值`helloString`应为"Hello"。  
  
## <a name="see-also"></a>请参阅  
 [如何：获取服务](../extensibility/how-to-get-a-service.md)   
 [使用并提供服务](../extensibility/using-and-providing-services.md)   
 [服务基础知识](../extensibility/internals/service-essentials.md)
