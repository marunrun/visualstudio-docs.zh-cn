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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435876"
---
# <a name="opening-a-dynamic-tool-window"></a>打开动态工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

从菜单中或等效的键盘快捷方式上的命令通常打开工具窗口。 有时，但是，您可能需要打开每当特定 UI 上下文应用，并关闭 UI 上下文不再适用时的工具窗口。 类似这样的工具窗口称为*动态*或*自动可见*。  
  
> [!NOTE]
> 预定义的 UI 上下文中的列表，请参阅<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>。 有关  
  
 如果你想要打开动态工具窗口在启动时，并可能创建失败，则必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx>接口，并测试中的失败条件<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A>方法。 为了使 shell 知道有一个动态工具窗口，应打开在启动时，必须添加`SupportsDynamicToolOwner`到包注册值 （设置为 1）。 此值不是标准的一部分<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>，因此必须创建要将其添加的自定义属性。 有关自定义特性的详细信息，请参阅[使用自定义注册特性注册扩展](../misc/using-a-custom-registration-attribute-to-register-an-extension.md)。  
  
 使用<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>打开工具窗口。 根据需要创建工具窗口。  
  
> [!NOTE]
> 可以由用户关闭动态工具窗口。 如果你想要创建菜单命令，以便用户可以重新打开工具窗口，应会打开工具窗口中，以及已禁用，否则为在同一 UI 上下文中启用菜单命令。  
  
### <a name="to-open-a-dynamic-tool-window"></a>若要打开动态工具窗口  
  
1. 创建一个名为的 VSIX 项目**DynamicToolWindow**并添加一个名为的工具窗口项模板**DynamicWindowPane.cs**。 有关详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
2. 在 DynamicWindowPanePackage.cs 文件中，找到 DynamicWindowPanePackage 声明。 添加<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>和 T:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute 属性注册工具窗口。  
  
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
  
     这将会注册后关闭并重新打开 Visual Studio 不会保持的瞬态窗口的称为 DynamicWindowPane 工具窗口。 打开 DynamicWindowPane 每当<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string>应用，并关闭否则。  
  
3. 生成项目并启动调试。 应显示在实验实例。 不应看到工具窗口。  
  
4. 在实验实例中打开一个项目。 应显示工具窗口。
