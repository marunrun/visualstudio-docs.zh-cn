---
title: 打开动态工具窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff971f980b0a9b2fb0e22f56fb0ace752829c2c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702264"
---
# <a name="open-a-dynamic-tool-window"></a>打开动态工具窗口
工具窗口通常从菜单上的命令或等效的键盘快捷键打开。 但是，有时您可能需要一个工具窗口，该窗口在应用特定 UI 上下文时打开，并在 UI 上下文不再应用时关闭。 这些类型的工具窗口称为*动态*或*自动可见*。

> [!NOTE]
> 有关预定义的 UI 上下文的列表，请参阅<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>。

 如果要在启动时打开动态工具窗口，并且创建可能失败，则必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx>接口并测试方法中的<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A>失败条件。 为了使 shell 知道在启动时应打开的动态工具窗口，必须将`SupportsDynamicToolOwner`值（设置为 1）添加到包注册中。 此值不是标准的<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>一部分，因此必须创建自定义属性来添加它。 有关自定义属性的详细信息，请参阅[使用自定义注册属性注册扩展](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension)。

 用于<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>打开工具窗口。 根据需要创建工具窗口。

> [!NOTE]
> 用户可以关闭动态工具窗口。 如果要创建菜单命令以便用户可以重新打开工具窗口，则应在打开工具窗口的相同 UI 上下文中启用菜单命令，否则将禁用该命令。

## <a name="to-open-a-dynamic-tool-window"></a>打开动态工具窗口

1. 创建名为**DynamicToolWindow 的**VSIX 项目，并添加名为*DynamicWindowPane.cs*的工具窗口项模板。 有关详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

2. 在*DynamicWindowPanePackage.cs*文件中，查找动态窗口窗格包声明。 添加<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>和<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>属性以注册工具窗口。

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

     上述属性将名为 DynamicWindowPane 的工具窗口注册为瞬态窗口，在 Visual Studio 关闭并重新打开时不会持久化。 动态窗口窗格在应用时<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string>打开，否则关闭。

3. 生成项目并启动调试。 应出现实验实例。 不应看到工具窗口。

4. 在实验实例中打开项目。 应显示工具窗口。
