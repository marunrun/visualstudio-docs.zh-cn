---
title: 项目配置对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e3321b70b51d194c67f1deee8ed33e240762b16b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725836"
---
# <a name="project-configuration-object"></a>项目配置对象
项目配置对象管理向 UI 显示配置信息。

 ![Visual Studio 项目配置](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg")项目配置属性页

 项目配置提供程序管理项目配置。 环境和其他包若要获取和检索有关项目配置的信息，请调用附加到项目配置提供程序对象的接口。

> [!NOTE]
> 不能以编程方式创建或编辑解决方案配置文件。 必须使用 `DTE.SolutionBuilder`。 有关详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

 若要发布要在配置 UI 中使用的显示名称，你的项目应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A>。 环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>，这将返回一个 `IVsCfg` 指针列表，你可以使用这些指针获取要在环境的 UI 中列出的配置和平台信息的显示名称。 活动配置和平台由存储在活动解决方案配置中的项目配置决定。 @No__t_0 方法可用于检索活动项目配置。

 可以选择在具有 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> 对象的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 对象上实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> 对象，以允许基于规范项目配置名称检索 `IVsProjectCfg2` 对象。

 向环境和其他项目提供对项目配置的访问的另一种方法是，项目提供 `IVsCfgProvider2::GetCfgs` 方法的实现以返回一个或多个配置对象。 项目还可能实现从 `IVsProjectCfg` 继承的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>，`IVsCfg` 从而提供特定于配置的信息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 支持平台和功能，以便添加、删除和重命名项目配置。

> [!NOTE]
> 由于 Visual Studio 不再限制为两个配置类型，因此不应在处理配置的情况下编写用于处理配置的代码，也不应假设只有一个项目配置必须是 "调试" 或 "零售"。 这使得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> 过时。

 对从 `IVsGetCfgProvider::GetCfgProvider` 返回的对象调用 `QueryInterface` 会检索 `IVsCfgProvider2`。 如果通过在 `IVsProject3` 项目对象上调用 `QueryInterface` 找不到 `IVsGetCfgProvider`，则可以通过在层次结构根浏览器对象上对为 `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)` 返回的对象调用 `QueryInterface`，或通过指向配置的指针来访问配置提供程序对象。为 `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)` 返回的提供程序。

 `IVsProjectCfg2` 主要提供对生成、调试和部署管理对象的访问，并允许项目自由地对输出进行分组。 @No__t_0 和 `IVsProjectCfg2` 的方法可用于实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> 来管理生成过程，并为配置的输出组 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> 指针。

 项目必须为其支持的每个配置返回相同数量的组，即使组中包含的输出数可能因配置而异。 组还必须具有与项目中的配置相同的标识符信息（规范名称、显示名称和组信息）。 有关详细信息，请参阅[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

 若要启用调试，你的配置应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>。 `IVsDebuggableProjectCfg` 是由项目实现的可选接口，该接口允许调试器启动配置，并在具有 `IVsCfg` 和 `IVsProjectCfg` 的配置对象上实现。 当用户按 F5 启动调试器时，环境将调用它。

 `ISpecifyPropertyPages` 和 `IDispatch` 与属性页结合使用，以便为用户检索和显示与配置相关的信息。 有关详细信息，请参阅[属性页](../../extensibility/internals/property-pages.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
- [属性页](../../extensibility/internals/property-pages.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)