---
title: 正在加载 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e20caff476e116ad59430692719bdbbe22c4914c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840512"
---
# <a name="loading-vspackages"></a>加载 VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

仅当需要功能时，Vspackage 才会加载到 Visual Studio 中。 例如，当 Visual Studio 使用项目工厂或 VSPackage 实现的服务时，将加载 VSPackage。 此功能称为延迟加载，尽可能使用它来提高性能。  
  
> [!NOTE]
> Visual Studio 可以确定某些 VSPackage 信息，如 VSPackage 提供的命令，而无需加载 VSPackage。  
  
 Vspackage 可以设置为特定用户界面中的 autoload (UI) 上下文（例如，当解决方案打开时）。 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>特性设置此上下文。  
  
### <a name="autoloading-a-vspackage-in-a-specific-context"></a>在特定上下文中自动加载 VSPackage  
  
- 将 `ProvideAutoLoad` 属性添加到 VSPackage 属性：  
  
    ```csharp  
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID  
    public class MyAutoloadedPackage : Package  
    {. . .}  
    ```  
  
     <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>有关 UI 上下文及其 GUID 值的列表，请参阅的枚举字段。  
  
- 在方法中设置断点 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 。  
  
- 生成 VSPackage 并启动调试。  
  
- 加载解决方案或创建一个解决方案。  
  
     VSPackage 加载并停止在断点处。  
  
## <a name="forcing-a-vspackage-to-load"></a>强制加载 VSPackage  
 在某些情况下，VSPackage 可能必须强制加载另一个 VSPackage。 例如，轻量 VSPackage 可能会将较大的 VSPackage 加载到不可作为 CMDUIContext 的上下文中。  
  
 您可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A> 方法强制加载 VSPackage。  
  
- 将此代码插入 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 强制另一个 VSPackage 加载的 VSPackage 的方法：  
  
    ```csharp  
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;  
    if (shell == null) return;  
  
    IVsPackage package = null;  
    Guid PackageToBeLoadedGuid =   
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);  
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);  
  
    ```  
  
     初始化 VSPackage 时，它将强制 `PackageToBeLoaded` 加载。  
  
     不应将强制加载用于 VSPackage 通信。 改为使用 [和提供服务](../extensibility/using-and-providing-services.md) 。  
  
## <a name="using-a-custom-attribute-to-register-a-vspackage"></a>使用自定义属性注册 VSPackage  
 在某些情况下，可能需要为扩展创建新的注册属性。 您可以使用注册属性来添加新的注册表项，或向现有的键添加新的值。 新特性必须派生自 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> ，并且它必须重写 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> 和 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> 方法。  
  
## <a name="creating-a-registry-key"></a>创建注册表项  
 在下面的代码中，自定义属性在要注册的 VSPackage 的注册表项下创建一个 **自定义** 子项。  
  
```csharp  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + @"}\Custom");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
    }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveKey(@"Packages\" + context.ComponentType.GUID + @"}\Custom");  
}  
  
```  
  
## <a name="creating-a-new-value-under-an-existing-registry-key"></a>在现有注册表项下创建新值  
 您可以向现有的键添加自定义值。 下面的代码演示如何将新值添加到 VSPackage 注册密钥。  
  
```csharp  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + "}");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
                }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveValue(@"Packages\" + context.ComponentType.GUID, "NewCustom");  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPackages](../extensibility/internals/vspackages.md)
