---
title: 加载 VSPackages |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439769"
---
# <a name="loading-vspackages"></a>加载 VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Vspackage 加载到 Visual Studio 中，仅当其功能是必需的。 例如，加载 VSPackage 时 Visual Studio 使用项目工厂或 VSPackage 实现的服务。 此功能被称为延迟的加载，这尽可能使用以提高性能。  
  
> [!NOTE]
> Visual Studio 可以确定某些 VSPackage 信息，例如 VSPackage 提供，而不加载 VSPackage 的命令。  
  
 Vspackage 可以设置为自动加载在特定的用户界面 (UI) 上下文中，例如，打开解决方案时。 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>属性将设置此上下文中。  
  
### <a name="autoloading-a-vspackage-in-a-specific-context"></a>自动加载 VSPackage 的特定上下文中  
  
- 添加`ProvideAutoLoad`VSPackage 属性的属性：  
  
    ```csharp  
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID  
    public class MyAutoloadedPackage : Package  
    {. . .}  
    ```  
  
     请参阅的枚举的字段<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>有关 UI 上下文及其 GUID 值的列表。  
  
- 中设置断点<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法。  
  
- 生成 VSPackage 并启动调试。  
  
- 加载解决方案或创建一个。  
  
     VSPackage 加载，并在断点处停止。  
  
## <a name="forcing-a-vspackage-to-load"></a>强制 VSPackage 加载  
 在某些情况下可能需要强制另一个 VSPackage 加载 VSPackage。 例如，轻型 VSPackage 可能会加载更大 VSPackage 中不能作为 CMDUIContext 的上下文。  
  
 可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A>方法，以强制 VSPackage 加载。  
  
- 插入此代码<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>强制另一个 VSPackage 加载的 vspackage 的方法：  
  
    ```csharp  
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;  
    if (shell == null) return;  
  
    IVsPackage package = null;  
    Guid PackageToBeLoadedGuid =   
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);  
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);  
  
    ```  
  
     初始化 VSPackage 时，它会强制`PackageToBeLoaded`加载。  
  
     强制加载不应该用于 VSPackage 通信。 使用[使用和提供服务](../extensibility/using-and-providing-services.md)相反。  
  
## <a name="using-a-custom-attribute-to-register-a-vspackage"></a>使用自定义属性来注册 VSPackage  
 在某些情况下可能需要创建新的注册属性为扩展插件。 若要添加新的注册表项或将新值添加到现有的密钥，可以使用注册属性。 新的属性必须派生自<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>，并且必须重写<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A>和<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A>方法。  
  
## <a name="creating-a-registry-key"></a>创建注册表项  
 在下面的代码中，创建自定义特性**自定义**子项下为其注册的 VSPackage 的键。  
  
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
  
## <a name="creating-a-new-value-under-an-existing-registry-key"></a>创建现有的注册表项下的新值  
 可以将自定义值添加到现有密钥。 下面的代码演示如何将新值添加到 VSPackage 注册密钥。  
  
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
  
## <a name="see-also"></a>请参阅  
 [VSPackage](../extensibility/internals/vspackages.md)
