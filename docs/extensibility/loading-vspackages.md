---
title: 正在加载 Vspackage |Microsoft Docs
description: 了解如何在 Visual Studio 中加载 Vspackage，包括延迟加载，尽可能使用它来提高性能。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 0aeab78a2f64be2df6f601ad8ed224f13071eb8c
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97616099"
---
# <a name="load-vspackages"></a>Load Vspackage
仅当需要功能时，Vspackage 才会加载到 Visual Studio 中。 例如，当 Visual Studio 使用项目工厂或 VSPackage 实现的服务时，将加载 VSPackage。 此功能称为延迟加载，尽可能使用它来提高性能。

> [!NOTE]
> Visual Studio 可以确定某些 VSPackage 信息，如 VSPackage 提供的命令，而无需加载 VSPackage。

 Vspackage 可以设置为特定用户界面中的 autoload (UI) 上下文（例如，当解决方案打开时）。 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>特性设置此上下文。

### <a name="autoload-a-vspackage-in-a-specific-context"></a>在特定上下文中 Autoload VSPackage

- 将 `ProvideAutoLoad` 属性添加到 VSPackage 属性：

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>有关 UI 上下文及其 GUID 值的列表，请参阅的枚举字段。

- 在方法中设置断点 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 。

- 生成 VSPackage 并启动调试。

- 加载解决方案或创建一个解决方案。

     VSPackage 加载并停止在断点处。

## <a name="force-a-vspackage-to-load"></a>强制加载 VSPackage
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

     不应将强制加载用于 VSPackage 通信。 请改用 [和提供服务](../extensibility/using-and-providing-services.md) 。

## <a name="see-also"></a>另请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
