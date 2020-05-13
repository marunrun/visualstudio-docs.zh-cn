---
title: 正在加载 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1c221bf06ef3b7e37e2afc1856f3e54fe5ad95e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702964"
---
# <a name="load-vspackages"></a>加载 VS 包
仅当需要 VS 包的功能时，才会加载到 Visual Studio 中。 例如，当 Visual Studio 使用项目工厂或 VSPackage 实现的服务时，将加载 VS 包。 此功能称为延迟加载，尽可能用于提高性能。

> [!NOTE]
> Visual Studio 可以确定某些 VSPackage 信息，例如 VSPackage 提供的命令，而无需加载 VSPackage。

 VS包可以设置为在特定用户界面 （UI） 上下文中自动加载，例如，当解决方案打开时。 属性<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>设置此上下文。

### <a name="autoload-a-vspackage-in-a-specific-context"></a>在特定上下文中自动加载 VS 包

- 将`ProvideAutoLoad`属性添加到 VSPackage 属性：

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     有关 UI 上下文及其<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>GUID 值的列表，请参阅 的枚举字段。

- 在<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法中设置断点。

- 生成 VS 包并开始调试。

- 加载解决方案或创建解决方案。

     VSPackage 在断点加载和停止。

## <a name="force-a-vspackage-to-load"></a>强制 VS 包加载
 在某些情况下，VSPackage 可能必须强制加载另一个 VSPackage。 例如，轻量级 VS 包可能会在无法作为 CMDUIContext 提供的上下文中加载较大的 VS 包。

 可以使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A>强制加载 VSPackage。

- 将此代码插入<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>VSPackage 的方法，该方法强制另一个 VSPackage 加载：

    ```csharp
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;
    if (shell == null) return;

    IVsPackage package = null;
    Guid PackageToBeLoadedGuid =
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);

    ```

     初始化 VSPackage 时，它将强制`PackageToBeLoaded`加载。

     力加载不应用于 VSPackage 通信。 而是[使用和提供服务](../extensibility/using-and-providing-services.md)。

## <a name="see-also"></a>请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
