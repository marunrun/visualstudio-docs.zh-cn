---
title: 自定义用户界面 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9d27fe21fb577f2e3610bf30109aa8c0b7f17a12
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312199"
---
# <a name="custom-user-interface-source-control-vspackage"></a>自定义用户界面 （源代码管理 VSPackage）
VSPackage 声明其菜单项和通过 Visual Studio 命令表及其默认状态 ( *.vsct*) 文件。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE) 在加载 VSPackage 之前为其默认状态显示的菜单项。 随后，<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>调用方法来启用或禁用菜单项。

 VSPackage 可以设置注册表项，因此可以根据命令用户界面 (UI) 上下文自动加载 VSPackage，尽管通常在进行源代码管理按需而不是只需切换到特定的 UI 上下文应该加载 VSPackage。 有关详细信息**AutoLoadPackages**注册表密钥，请参阅[管理 Vspackage](../../extensibility/managing-vspackages.md)。

## <a name="vspackage-ui"></a>VSPackage UI
 源代码管理包作为 VSPackage 实现，并且不使用任何 UI 中的从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 每个源代码管理 VSPackage 必须指定其自己的 UI 元素，如菜单项、 菜单组中，工具窗口、 工具栏和任何必需的 UI 选项特定于设置源代码管理 VSPackage。 可以启用这些 UI 元素，静态或动态。 静态 UI 元素中定义 *.vsct*文件，或未加载 VSPackage 是否显示。 动态 UI 元素可能是可见具体取决于特定命令 UI 上下文，如<xref:EnvDTE.Constants.vsContextNoSolution>，或作为对的调用结果<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法。 动态 UI 元素的可见性将遵循的 Vspackage 的延迟加载的策略。

## <a name="ui-constraints-on-source-control-vspackages"></a>源代码管理 Vspackage 的 UI 约束
 因为无法从 IDE 删除源代码管理 VSPackage，加载后，VSPackage 必须能进入非活动状态。 当 VSPackage 收到通知，它不再处于活动状态时，VSPackage 中禁用其 UI，并忽略任何外部 IDE 交互。 VSPackage 的实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>VSPackage 未处于活动状态时，方法应隐藏命令。

 每个源代码管理 VSPackage 必须实现`IVsSccProvider`接口。 在接口上的两种方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>，VSPackage 必须实现。

 源代码管理 VSPackage 可能已订阅各种 IDE 事件，由实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>， <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>，依次类推。 此外，VSPackage 可能已实现启用注册表的回调接口，如<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>。 这些接口必须全部时忽略非活动状态。

 以下列表显示受源代码管理 VSPackage 的活动状态的接口：

- 跟踪项目文档的事件。

- 解决方案的事件。

- 解决方案持久性接口。 当非活动状态时，包应写入 *.sln*并 *.suo*文件。

- 属性扩展程序。

  所需<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>，并且还与源控件关联的任何可选接口时，不调用源代码管理 VSPackage 处于非活动状态。

  当[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 启动[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]命令 UI 上下文设置为当前默认的源代码管理 VSPackage id。 ID 这会导致活动的源控件要显示在 IDE 中，而不实际加载 VSPackage 的 VSPackage 的静态 UI。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 注册为暂停[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>使得对 VSPackage 的任何调用之前。

  下表介绍了有关的特定详细信息[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不同 UI 项，IDE 将隐藏。

| UI 项 | 描述 |
| - | - |
| 菜单和工具栏 | 源代码管理包必须设置为中的源控制包 ID 的初始菜单和工具栏可见性状态[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)一部分 *.vsct*文件。 这使得[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 适当地设置菜单项的状态而无需加载 VSPackage 和调用的实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>方法。 |
| 工具窗口 | 源代码管理 VSPackage 隐藏进行非活动状态时它拥有任何工具窗口。 |
| 源代码管理 VSPackage 特定选项页 | 注册表项**HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts**允许 VSPackage 设置在其中它要求其选项页中显示的上下文。 此密钥下的注册表项必须通过使用服务 ID (SID) 的源代码管理服务并将其分配 DWORD 值 1 创建。 每次在上下文中源代码管理 VSPackage 注册，UI 事件发生时，如果它处于活动状态，将会调用 VSPackage。 |

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [管理 VSPackages](../../extensibility/managing-vspackages.md)