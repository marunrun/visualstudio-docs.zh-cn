---
title: 自定义用户界面（源控制 VS 包） |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708932"
---
# <a name="custom-user-interface-source-control-vspackage"></a>自定义用户界面（源代码管理 VS 包）
VSPackage 通过 Visual Studio 命令表 *（.vsct*） 文件声明其菜单项及其默认状态。 集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]开发环境 （IDE） 以默认状态显示菜单项，直到加载 VSPackage。 随后，调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>该方法以启用或禁用菜单项。

 VSPackage 可以设置注册表项，以便 VSPackage 可以根据命令用户界面 （UI） 上下文自动加载，尽管通常源代码管理 VSPackage 应按需加载，而不是仅切换到特定的 UI 上下文。 有关**自动加载包**注册表项的详细信息，请参阅[管理 VS 包](../../extensibility/managing-vspackages.md)。

## <a name="vspackage-ui"></a>VSPackage UI
 源代码管理包作为 VSPackage 实现，不使用 中的任何[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI。 每个源代码管理 VSPackage 必须指定其自己的 UI 元素，如菜单项、菜单组、工具窗口、工具栏和任何所需的 UI 来设置特定于源代码管理 VSPackage 的选项。 这些 UI 元素可以静态或动态启用。 静态 UI 元素在 *.vsct*文件中定义，无论是否加载 VS 包，都显示。 动态 UI 元素可能可见，具体取决于特定命令 UI 上下文（<xref:EnvDTE.Constants.vsContextNoSolution>如 ）或由于对<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法调用的结果。 动态 UI 元素的可见性符合延迟加载 VS 包的策略。

## <a name="ui-constraints-on-source-control-vspackages"></a>源代码管理 VSPackages 上的 UI 约束
 由于源控件 VSPackage 在加载后无法从 IDE 中删除，因此 VSPackage 必须能够进入非活动状态。 当 VS 包收到其不再处于活动状态的通知时，VS包将禁用其 UI 并忽略任何外部 IDE 交互。 当 VSPackage 不处于活动状态时<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>，VSPackage 的方法的实现应隐藏命令。

 每个源代码管理 VSPackage 都必须`IVsSccProvider`实现接口。 接口上的两种方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>必须由 VSPackage 实现。

 源代码管理 VSPackage 可能已订阅了各种 IDE 事件，这些事件由<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>等实现。 此外，VSPackage 可能已实现启用注册表的回调接口，<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>例如 。 这些接口都必须在非活动时被忽略。

 下面的列表显示受源代码管理 VSPackage 的活动状态影响的接口：

- 跟踪项目文档事件。

- 解决方案事件。

- 解决方案持久性接口。 当处于非活动状态时，包不应写入 *.sln*和 *.suo*文件。

- 属性扩展器。

  当源代码<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>管理<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>VSPackage 处于非活动状态时，不会调用所需的 和 以及与源代码管理关联的任何可选接口。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]当 IDE 启动[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时，将命令 UI 上下文设置为当前默认源控件 VSPackage ID 的 ID。 这将导致活动源控件 VSPackage 的静态 UI 显示在 IDE 中，而无需实际加载 VSPackage。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]暂停 VSPackage 在对 VSPackage 进行任何调用之前[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过 注册<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>。

  下表描述了有关[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 如何隐藏不同 UI 项的具体详细信息。

| UI 项 | 描述 |
| - | - |
| 菜单和工具栏 | 源代码管理包必须在 *.vsct*文件的[可见性约束](../../extensibility/visibilityconstraints-element.md)部分中将初始菜单和工具栏可见性状态设置为源代码管理包 ID。 这使[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 能够适当地设置菜单项的状态，而无需加载 VSPackage 并调用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法的实现。 |
| 工具窗口 | 源代码管理 VSPackage 隐藏它位于非活动状态时拥有的任何工具窗口。 |
| 源代码管理 VSPackage 特定选项页 | 注册表项**HKLM_SOFTWARE_Microsoft_VisualStudio_X.Y_ToolsOptionsPages_可见性CmdUIContexts**允许 VSPackage 设置它需要显示其选项页的上下文。 必须使用此密钥下的注册表项使用源代码管理服务的服务 ID （SID） 并为其分配 DWORD 值 1。 每当在注册源代码管理 VSPackage 的上下文中发生 UI 事件时，如果 VSPackage 处于活动状态，则将调用它。 |

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [管理 VSPackage](../../extensibility/managing-vspackages.md)
