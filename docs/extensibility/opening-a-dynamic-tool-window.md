---
title: 打开动态工具窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dfb00665caae499c0088f4ba5163c85ffacdbd85
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336263"
---
# <a name="open-a-dynamic-tool-window"></a>打开动态工具窗口
从菜单中或等效的键盘快捷方式上的命令通常打开工具窗口。 有时，但是，您可能需要打开每当特定 UI 上下文应用，并关闭 UI 上下文不再适用时的工具窗口。 工具窗口的这些类型称为*动态*或*自动可见*。

> [!NOTE]
> 预定义的 UI 上下文中的列表，请参阅<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>。

 如果你想要打开动态工具窗口在启动时，并可能创建失败，则必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx>接口，并测试中的失败条件<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A>方法。 为了使 shell 知道有一个动态工具窗口，应打开在启动时，必须添加`SupportsDynamicToolOwner`到包注册值 （设置为 1）。 此值不是标准的一部分<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>，因此必须创建要将其添加的自定义属性。 有关自定义特性的详细信息，请参阅[使用自定义注册特性注册扩展](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension)。

 使用<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>打开工具窗口。 根据需要创建工具窗口。

> [!NOTE]
> 可以由用户关闭动态工具窗口。 如果你想要创建菜单命令，以便用户可以重新打开工具窗口，应会打开工具窗口中，以及已禁用，否则为在同一 UI 上下文中启用菜单命令。

## <a name="to-open-a-dynamic-tool-window"></a>若要打开动态工具窗口

1. 创建一个名为的 VSIX 项目**DynamicToolWindow**并添加一个名为的工具窗口项模板*DynamicWindowPane.cs*。 有关详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

2. 在中*DynamicWindowPanePackage.cs*文件中，找到 DynamicWindowPanePackage 声明。 添加<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>和<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>属性注册工具窗口。

    ```vb
    [ProvideToolWindow(typeof(DynamicWindowPane)]
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]
    [Guid(DynamicWindowPanePackage.PackageGuidString)]
    public sealed class DynamicWindowPanePackage : Package
    {. . .}
    ```

     以上属性注册后关闭并重新打开 Visual Studio 不会保持的瞬态窗口的称为 DynamicWindowPane 工具窗口。 打开 DynamicWindowPane 每当<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string>应用，并关闭否则。

3. 生成项目并启动调试。 应显示在实验实例。 不应看到工具窗口。

4. 在实验实例中打开一个项目。 应显示工具窗口。