---
title: 项目配置对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 001509b56e3bac6a8fd585eb0efe0bd57018acea
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706659"
---
# <a name="project-configuration-object"></a>项目配置对象
项目配置对象管理向 UI 显示配置信息。

 ![Visual Studio 项目配置](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg") 项目配置属性页

 项目配置提供程序管理项目配置。 环境和其他包若要获取和检索有关项目配置的信息，请调用附加到项目配置提供程序对象的接口。

> [!NOTE]
> 不能以编程方式创建或编辑解决方案配置文件。 您必须使用 `DTE.SolutionBuilder`。 有关详细信息，请参阅 [解决方案配置](../../extensibility/internals/solution-configuration.md) 。

 若要发布要在配置 UI 中使用的显示名称，你的项目应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A> 。 环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> ，它将返回一个指针列表， `IVsCfg` 你可以使用该列表来获取要在环境的 UI 中列出的配置和平台信息的显示名称。 活动配置和平台由存储在活动解决方案配置中的项目配置决定。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A>方法可用于检索活动的项目配置。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>可以选择使用对象在对象上实现对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> ，以允许您 `IVsProjectCfg2` 基于规范项目配置名称检索对象。

 向环境和其他项目提供对项目配置的访问的另一种方法是，项目提供方法的实现 `IVsCfgProvider2::GetCfgs` 以返回一个或多个配置对象。 项目还可以实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> ，它们继承自 `IVsProjectCfg` `IVsCfg` ，进而提供特定于配置的信息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 支持平台和功能，以便添加、删除和重命名项目配置。

> [!NOTE]
> 由于 Visual Studio 不再限制为两个配置类型，因此不应在处理配置的情况下编写处理配置的代码，也不应假定只有一个配置的项目必须是调试或零售。 这会使使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> 过时。

 `QueryInterface`对从检索返回的对象 `IVsGetCfgProvider::GetCfgProvider` 调用 `IVsCfgProvider2` 。 如果 `IVsGetCfgProvider` 通过对项目对象调用来找不到 `QueryInterface` `IVsProject3` ，则可以通过对 `QueryInterface` 返回的对象的层次结构根浏览器对象调用 `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)` ，或通过指向为返回的配置提供程序的指针来访问配置提供程序对象 `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)` 。

 `IVsProjectCfg2` 主要提供对生成、调试和部署管理对象的访问，并允许项目自由地对输出进行分组。 和的方法 `IVsProjectCfg` `IVsProjectCfg2` 可用于实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> 以管理生成过程，并使用指针来管理 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> 配置的输出组。

 项目必须为其支持的每个配置返回相同数量的组，即使组中包含的输出数可能因配置而异。 组还必须具有相同的标识符信息 (规范名称、显示名称和组信息) 从配置到项目中的配置。 有关详细信息，请参阅 [输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

 若要启用调试，你的配置应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> 。 `IVsDebuggableProjectCfg` 是由项目实现的可选接口，该接口允许调试器启动配置，并使用和在配置对象上实现 `IVsCfg` `IVsProjectCfg` 。 当用户按 F5 启动调试器时，环境将调用它。

 `ISpecifyPropertyPages` 和 `IDispatch` 将与属性页结合使用，以便为用户检索和显示与配置相关的信息。 有关详细信息，请参阅 [属性页](../../extensibility/internals/property-pages.md)。

## <a name="see-also"></a>另请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
- [属性页](../../extensibility/internals/property-pages.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
