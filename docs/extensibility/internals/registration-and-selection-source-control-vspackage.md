---
title: 注册和选择 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9bb993f6acaa7cd1cf3980e128e869a643d028c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310909"
---
# <a name="registration-and-selection-source-control-vspackage"></a>注册和选择（源代码管理 VSPackage）
源代码管理 VSPackage 必须注册才能公开到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 如果注册了多个源代码管理 VSPackage，用户可以选择在适当的时候加载的 VSPackage。 请参阅[Vspackage](../../extensibility/internals/vspackages.md)有关 Vspackage 以及如何将它们注册的更多详细信息。

## <a name="registering-a-source-control-package"></a>注册源代码管理包
 源代码管理包已注册，以便[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境可以找到它，并查询其支持的功能。 这是根据其功能或命令所需或显式请求时，仅在其中创建包的实例的延迟加载方案。

 Vspackage 将信息放在一个特定于版本的注册表项，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y*，其中*X*是主版本号和*Y*是次版本号。 这种做法提供支持的多个版本的并行安装的功能[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]用户界面 (UI) 以及源代码管理 Vspackage 支持从多个安装的源代码管理插件 （通过源控件适配器包） 中进行选择。 可以有一个活动的源代码管理插件或 VSPackage 一次。 但是，如下所述，IDE 会允许通过自动基于解决方案的包交换机制源代码控制插件和 Vspackage 之间切换。 有一些部分源代码管理 VSPackage 的要求，若要启用此选择机制。

### <a name="registry-entries"></a>注册表项
 源代码管理包需要三个专用 Guid:

- 包 GUID:这是包含 （在本部分中称为 ID_Package） 的源控件实现的包的主要 GUID。

- 源控件 GUID:这是个源代码管理用于将注册 Visual Studio 源控件存根的 VSPackage 的 GUID，也可用作命令 UI 上下文的 GUID。 源代码管理 GUID 注册时源代码管理服务的 GUID。 在示例中，源控件 GUID 称为 ID_SccProvider。

- 源代码管理服务的 GUID:这是专用的服务 （在本部分中称为 SID_SccPkgService） 的 Visual Studio 使用的 GUID。 除此之外，源代码管理包需要定义其他 Guid 的 Vspackage，工具窗口，依次类推。

  必须由源代码管理 VSPackage 进行以下注册表项：

| 项名称 | 条目 |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | (default) = rg_sz:{ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | （默认值） = rg_sz:\<包的友好名称 ><br /><br /> Service = rg_sz:{SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | （默认值） = rg_sz: #\<本地化名称的资源 ID ><br /><br /> Package = rg_sz:{ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (请注意，键名称， `SourceCodeControl`，已由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不是可用的选择和\<包名称 >。) | （默认值） = rg_sz: {ID_Package} |

## <a name="selecting-a-source-control-package"></a>选择源代码管理包
 多个基于源控制插件 API 的即插即用的项和源代码的控制可能同时注册 Vspackage。 选择 VSPackage 或源代码管理插件的过程必须确保[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载插件或 VSPackage 在适当的时间，并可以推迟加载不必要的组件，直到它们是必需的。 此外，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]必须从其他非活动状态的 Vspackage，包括菜单项、 对话框和工具栏，删除所有 UI 并显示为活动的 VSPackage 的 UI。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 将源代码管理 VSPackage 加载时执行以下操作之一：

- （当解决方案处于源代码管理下），打开解决方案。

   打开解决方案或项目受源代码管理时，IDE 会导致源代码管理 VSPackage 已指定为要加载该解决方案。

- 执行任何源代码管理 VSPackage 的菜单命令。

  仅当它们实际上将会需要的任何组件应该加载 VSPackage 的源控件使用 （也称为延迟加载）。

### <a name="automatic-solution-based-vspackage-swapping"></a>自动基于解决方案的 VSPackage 交换
 你可以手动交换源代码管理 Vspackage 通过[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**选项**对话框中的下**源代码管理**类别。 基于解决方案的包自动交换意味着打开该解决方案时，已被指定为特定解决方案的源代码管理包会自动设置为处于活动状态。 每个源代码管理包应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 处理两者之间切换源代码管理插件 （实现源控件插件 API） 和源代码管理 Vspackage。

 源控件适配器包用于切换到任何基于源控制插件 API 的插件。 切换到中间的源控件适配器包和确定哪些源代码管理插件的过程必须设置为活动或非活动用户是透明的。 适配器包始终处于活动状态的任何源代码管理插件处于活动状态时。 两个源控制插件相当于只需加载和卸载插件 DLL 之间进行切换。 切换到源代码管理 VSPackage，但是，涉及到与 IDE 加载相应的 VSPackage 进行交互。

 源代码管理 VSPackage 时，调用打开任何解决方案和 VSPackage 的注册表项是在解决方案文件。 打开解决方案时，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]查找注册表值并加载相应的源代码管理 VSPackage。 所有源代码管理 Vspackage 必须都具有上面所述的注册表项。 源代码管理下的解决方案被标记为与特定的源代码管理 VSPackage 关联。 源代码的管理 Vspackage 必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>若要启用自动基于解决方案的 VSPackage 交换。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>Visual Studio 包选择和切换用户界面
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供了源代码管理 VSPackage 的 UI 和插件中的所选内容**选项**对话框中的下**源代码管理**类别。 它允许用户选择活动的源代码管理插件或 VSPackage。 下拉列表包括：

- 所有已安装的源代码管理包

- 所有安装的源代码管理插件

- "None"选项，它表示禁用源代码管理

  仅选择此活动的源控件的 UI 是可见的。 VSPackage 选择上一个 vspackage 隐藏 UI，并显示新的 UI。 活动的 VSPackage 选择基于每个用户。 如果用户具有的多个副本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]同时打开，每个有可能使用不同的 active VSPackage。 如果多个用户在登录到同一台计算机，每个用户可以拥有的单独实例[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]打开每个都有不同的 active VSPackage。 当多个实例[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]关闭的用户，源代码管理 VSPackage 的最后一个打开的解决方案将成为默认的源代码管理 VSPackage，若要设置活动上重新启动处于活动状态。

  与以前版本的不同[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，IDE 重新启动，则不能再切换源代码管理 Vspackage 的唯一方法。 VSPackage 选择是自动的。 切换包需要 Windows 用户权限 （没有管理员或超级用户）。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [功能](../../extensibility/internals/source-control-vspackage-features.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackage](../../extensibility/internals/vspackages.md)