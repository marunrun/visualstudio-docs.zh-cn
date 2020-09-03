---
title: " (源代码管理的自定义用户界面) |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6ef807cef17a6ca3cddfee05ba57ace27e34a9e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708932"
---
# <a name="custom-user-interface-source-control-vspackage"></a> (源代码管理的自定义用户界面 VSPackage) 
VSPackage 通过 Visual Studio 命令 *表) 文件* (声明其菜单项及其默认状态。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 在加载 VSPackage 之前显示处于默认状态的菜单项。 然后， <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 调用方法以启用或禁用菜单项。

 VSPackage 可以设置一个注册表项，以便可以根据命令用户界面 (UI) 上下文来自动加载 VSPackage，尽管通常会按需加载源代码管理，而不是只是切换到特定的 UI 上下文。 有关 **AutoLoadPackages** 注册表项的详细信息，请参阅 [Manage vspackage](../../extensibility/managing-vspackages.md)。

## <a name="vspackage-ui"></a>VSPackage UI
 源代码管理包作为 VSPackage 实现，不使用中的任何 UI [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 每个源代码管理 VSPackage 必须指定其自己的 UI 元素，例如菜单项、菜单组、工具窗口、工具栏以及设置特定于源代码管理 VSPackage 的选项所需的任何 UI。 这些 UI 元素可以静态或动态地启用。 静态 UI 元素在 *.vsct* 文件中定义，并显示 VSPackage 是否已加载。 动态 UI 元素可能会显示，具体取决于特定的命令 UI 上下文（例如 <xref:EnvDTE.Constants.vsContextNoSolution> ），或作为调用方法的结果 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 。 动态 UI 元素的可见性符合 Vspackage 的延迟加载策略。

## <a name="ui-constraints-on-source-control-vspackages"></a>源代码管理 Vspackage 的 UI 约束
 由于源控件 VSPackage 在加载后无法从 IDE 中删除，因此 VSPackage 必须能够进入非活动状态。 当 VSPackage 收到不再处于活动状态的通知时，VSPackage 将禁用其 UI，并忽略任何外部 IDE 交互。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>当 VSPackage 处于非活动状态时，该方法的 VSPackage 实现应隐藏命令。

 每个源代码管理 VSPackage 都必须实现 `IVsSccProvider` 接口。 接口上的两个方法（ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> ）必须由 VSPackage 实现。

 源代码管理 VSPackage 可能已订阅各种 IDE 事件，这些事件由、等实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 。 此外，VSPackage 可能已实现启用注册表的回调接口，如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 。 在非活动状态时，必须忽略这些接口。

 下面的列表显示受源代码管理 VSPackage 的活动状态影响的接口：

- 跟踪项目文档事件。

- 解决方案事件。

- 解决方案持久性接口。 如果不活动，包不应写入 *.sln* 和 *.suo* 文件中。

- 属性扩展程序。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 源代码管理 VSPackage 处于非活动状态时，不会调用所需的和以及与源控件关联的任何可选接口。

  当 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 启动时， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 将命令 UI 上下文设置为当前默认源代码管理 VSPackage ID 的 id。 这将导致活动源代码管理 VSPackage 的静态 UI 在 IDE 中显示，而不会实际加载 VSPackage。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 暂停，以便在对 VSPackage 进行 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> 任何调用之前通过注册。

  下表介绍有关 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 如何隐藏不同 UI 项的特定详细信息。

| UI 项 | 说明 |
| - | - |
| 菜单和工具栏 | 源代码管理包必须在 *.vsct*文件的[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)节中将初始菜单和工具栏可见性状态设置为源代码管理包 ID。 这使 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 可以适当地设置菜单项的状态，而无需加载 VSPackage 和调用方法的实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 。 |
| 工具窗口 | 当激活时，源代码管理 VSPackage 将隐藏它拥有的任何工具窗口。 |
| 源代码管理 VSPackage 特定的选项页 | 使用注册表项 **HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts** ，VSPackage 可以设置在其中显示其选项页的上下文。 此项下的注册表项必须使用源代码管理服务的服务 ID (SID) 来创建，并为其分配 DWORD 值1。 每当在 VSPackage 中向其注册源代码管理的上下文中发生 UI 事件时，如果该 VSPackage 处于活动状态，就会调用它。 |

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [管理 VSPackage](../../extensibility/managing-vspackages.md)
