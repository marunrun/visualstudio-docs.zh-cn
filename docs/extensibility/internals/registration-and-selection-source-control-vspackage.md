---
title: 注册和选择（源控制 VS 包） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 973eb19916a737dfa775fe79ee62cb3d11fe0123
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705722"
---
# <a name="registration-and-selection-source-control-vspackage"></a>注册和选择（源代码管理 VSPackage）
必须注册源代码管理 VSPackage 才能将其公开给[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 如果注册了多个源代码管理 VSPackage，用户可以选择在适当时间加载的 VSPackage。 有关[VSPackages](../../extensibility/internals/vspackages.md)以及如何注册它们的更多详细信息，请参阅 VS 包。

## <a name="registering-a-source-control-package"></a>注册源代码管理包
 源控件包已注册，以便[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境可以找到它并查询其支持的功能。 这符合延迟加载方案，其中仅在需要或显式请求包的功能或命令时创建包实例。

 VS包将信息放在特定于版本的注册表项中\\，HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio*X.Y，* 其中*X*是主要版本号 *，Y*是次要版本号。 这种做法提供了支持并行安装多个版本的 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]功能。

 用户界面[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]（UI） 支持从多个已安装的源代码管理插件（通过源代码管理适配器包）和源代码管理 VSPackage 中进行选择。 一次只能有一个活动源代码管理插件或 VSPackage。 但是，如下所述，IDE 允许通过基于解决方案的自动包交换机制在源代码管理插件和 VSPackage 之间切换。 源代码管理 VSPackage 有一些要求来启用此选择机制。

### <a name="registry-entries"></a>注册表项
 源代码管理包需要三个专用 GUID：

- 包 GUID：这是包含源代码管理实现（本节中称为ID_Package）的包的主要 GUID。

- 源代码管理 GUID：这是用于向可视化工作室源代码管理存根注册的源代码管理 VSPackage 的 GUID，也可用作命令 UI 上下文 GUID。 源代码管理服务 GUID 在源代码管理 GUID 下注册。 在此示例中，源控件 GUID 称为ID_SccProvider。

- 源代码管理服务 GUID：这是 Visual Studio 使用的专用服务 GUID（本节中称为SID_SccPkgService）。 除此之外，源代码管理包还需要为 VSPackage、工具窗口等定义其他 GUID。

  以下注册表项必须由源代码管理 VSPackage 进行：

| 项名 | 条目 |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | （默认） = rg_sz：[ID_SccProvider] |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | （默认） =\<rg_sz：包>的友好名称<br /><br /> 服务 = rg_sz：[SID_SccPkgService] |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | （默认） = rg_sz：*\<本地化名称的资源 ID><br /><br /> 包 = rg_sz：[ID_Package] |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> （请注意，密钥名称`SourceCodeControl`、 已由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和 不可用作为\<包名称>的选择。 | （默认） = rg_sz：[ID_Package] |

## <a name="selecting-a-source-control-package"></a>选择源代码管理包
 可以同时注册多个基于源代码管理插件的插件插件和源代码管理 VS 包。 选择源代码管理插件或 VSPackage 的过程必须确保在适当的时间[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载插件或 VSPackage，并可以延迟加载不必要的组件，直到需要它们。 此外，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]必须从其他非活动 VS 包中删除所有 UI，包括菜单项、对话框和工具栏，并显示活动 VSPackage 的 UI。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]执行以下任一操作时，加载源代码管理 VSPackage：

- 解决方案打开（当解决方案处于源代码控制之下时）。

   打开源代码管理下的解决方案或项目时，IDE 会导致加载为该解决方案指定的源代码管理 VSPackage。

- 将执行源代码管理 VSPackage 的任何菜单命令。

  源代码管理 VSPackage 应仅在实际使用组件（也称为延迟加载）时加载其所需的任何组件。

### <a name="automatic-solution-based-vspackage-swapping"></a>基于解决方案的自动 VS 包交换
 您可以通过 **"源控制**"类别下的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**"选项**"对话框手动交换源代码管理 VS 包。 基于解决方案的自动包交换意味着在打开该解决方案时，已为特定解决方案指定的源代码管理包将自动设置为活动。 每个源代码管理包都应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>和 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]处理源代码管理插件（实现源代码管理插件 API）和源代码管理 VS 包之间的交换机。

 源代码管理适配器包用于切换到任何基于源代码管理插件的插件 API。 切换到中间源代码管理适配器包并确定必须设置为活动或非活动的源代码管理插件的过程对用户是透明的。 当任何源代码管理插件处于活动状态时，适配器包始终处于活动状态。 在两个源代码管理插件之间切换只需加载和卸载插件 DLL 即可。 但是，切换到源代码管理 VSPackage 需要与 IDE 交互以加载相应的 VSPackage。

 当打开任何解决方案并且 VSPackage 的注册表项位于解决方案文件中时，将调用源代码管理 VSPackage。 打开解决方案后，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]查找注册表值并加载相应的源代码管理 VSPackage。 所有源代码管理 VS包必须具有上述注册表项。 受源代码管理的解决方案被标记为与特定的源代码管理 VSPackage 相关联。 源代码管理 VSPackage 必须<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>实现 实现，以启用基于解决方案的自动 VSPackage 交换。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>用于包选择和切换的可视化工作室 UI
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在 **"源控制**"类别下的 **"选项**"对话框中为源代码管理 VSPackage 和插件选择提供了 UI。 它允许用户选择活动源控制插件或 VSPackage。 下拉列表包括：

- 所有已安装的源代码管理包

- 所有已安装的源代码管理插件

- 禁用源代码控制的"无"选项

  只有活动源代码管理选择的 UI 可见。 VSPackage 选择隐藏上一个 VSPackage 的 UI，并显示新 VSPackage 的 UI。 活动 VS 包是按用户选择的。 如果用户具有多个同时打开的副本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，则每个副本可能使用不同的活动 VS 包。 如果多个用户登录到同一台计算机，则每个用户可以具有单独的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]打开实例，每个实例具有不同的活动 VSPackage。 当用户关闭 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]多个实例时，为最后一个打开的解决方案处于活动状态的源代码管理 VSPackage 将成为默认源代码管理 VSPackage，在重新启动时设置为活动。

  与 的早期版本不同[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，IDE 重新启动不再是切换源代码管理 VSPackages 的唯一方法。 VSPackage 选择是自动的。 切换包需要 Windows 用户权限（不是管理员或超级用户）。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [功能](../../extensibility/internals/source-control-vspackage-features.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackage](../../extensibility/internals/vspackages.md)
