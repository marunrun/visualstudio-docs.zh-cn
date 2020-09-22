---
title: 打开动态工具窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09b81294abc708cf7616dad03b5dd7333d6a1719
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840644"
---
# <a name="opening-a-dynamic-tool-window"></a>打开动态工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

工具窗口通常从菜单上的命令或等效的键盘快捷方式打开。 但是，有时您可能需要在应用特定 UI 上下文时打开的工具窗口，并在 UI 上下文不再适用时关闭。 这样的工具窗口称为 " *动态* " 或 " *自动可见*"。  
  
> [!NOTE]
> 有关预定义 UI 上下文的列表，请参阅 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> 。 对于“组名称”  
  
 如果要在启动时打开动态工具窗口，并且创建可能会失败，则必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> 接口，并在方法中测试失败条件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> 。 为了使 shell 知道您有一个应在启动时打开的动态工具窗口，必须将 `SupportsDynamicToolOwner` 值 (设置为 1) 添加到包注册中。 此值不是标准的一部分 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> ，因此你必须创建自定义属性来添加它。 有关自定义特性的详细信息，请参阅 [使用自定义注册特性注册扩展](../misc/using-a-custom-registration-attribute-to-register-an-extension.md)。  
  
 使用 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> 打开工具窗口。 将根据需要创建工具窗口。  
  
> [!NOTE]
> 用户可以关闭动态工具窗口。 如果要创建菜单命令以使用户能够重新打开工具窗口，则应在打开工具窗口的同一 UI 上下文中启用菜单命令，否则，将禁用。  
  
### <a name="to-open-a-dynamic-tool-window"></a>打开动态工具窗口  
  
1. 创建名为 **DynamicToolWindow** 的 VSIX 项目，并添加名为 **DynamicWindowPane.cs**的工具窗口项模板。 有关详细信息，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
2. 在 DynamicWindowPanePackage.cs 文件中，找到 DynamicWindowPanePackage 声明。 添加 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 和 T:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute 属性以注册工具窗口。  
  
    ```vb  
    [[ProvideToolWindow(typeof(DynamicWindowPane)]  
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]  
    [Guid(DynamicWindowPanePackageGuids.PackageGuidString)]  
    public sealed class DynamicWindowPanePackage : Package  
    {. . .}  
    ```  
  
     这会将名为 DynamicWindowPane 的工具窗口注册为一个临时窗口，该窗口在关闭并重新打开 Visual Studio 时不会保持。 DynamicWindowPane 会在应用时打开 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> ，否则将会关闭。  
  
3. 生成项目并启动调试。 应显示实验实例。 你将看不到工具窗口。  
  
4. 在实验实例中打开一个项目。 应显示工具窗口。
