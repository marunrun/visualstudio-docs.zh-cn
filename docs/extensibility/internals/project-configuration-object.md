---
title: 项目配置对象 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706659"
---
# <a name="project-configuration-object"></a>项目配置对象
项目配置对象管理向 UI 显示配置信息。

 ![可视化工作室项目配置](../../extensibility/internals/media/vsprojectcfg.gif "vs 项目Cfg")项目配置属性页

 项目配置提供程序管理项目配置。 若要访问和检索有关项目配置的信息，环境和其他包调用附加到项目配置提供程序对象的接口。

> [!NOTE]
> 无法以编程方式创建或编辑解决方案配置文件。 您必须使用 `DTE.SolutionBuilder`。 有关详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

 要发布要在配置 UI 中使用的显示名称，项目应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A>。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>，它返回可用于获取要`IVsCfg`在环境 UI 中列出的配置和平台信息的显示名称的指针列表。 活动配置和平台由存储在活动解决方案配置中的项目配置决定。 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A>可用于检索活动项目配置。

 对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>可以选择在<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>对象上与对象一起实现，<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper>以允许您基于规范项目配置名称检索`IVsProjectCfg2`对象。

 向环境和其他项目提供项目配置访问权限的另一种方法是，项目提供方法的`IVsCfgProvider2::GetCfgs`实现以返回一个或多个配置对象。 项目还可以实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>，从 继承 ，`IVsProjectCfg`从而从`IVsCfg`中继承 ， 以提供特定于配置的信息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>支持用于添加、删除和重命名项目配置的平台和功能。

> [!NOTE]
> 由于 Visual Studio 不再局限于两种配置类型，因此处理配置的代码不应与配置数量的假设一起编写，也不应假定只有一个配置的项目必然是调试或零售。 这使得使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A>过时。

 调用`QueryInterface`从`IVsGetCfgProvider::GetCfgProvider`检索返回的对象`IVsCfgProvider2`。 如果`IVsGetCfgProvider`通过调用`QueryInterface``IVsProject3`项目对象找不到，则可以通过调用`QueryInterface`返回`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)`的对象的层次结构根浏览器对象或通过指向 返回的配置提供程序的`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)`指针来访问配置提供程序对象。

 `IVsProjectCfg2`主要提供对生成、调试和部署管理对象的访问，并允许项目自由分组输出。 的方法`IVsProjectCfg``IVsProjectCfg2`可用于实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>管理生成过程，以及<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup>配置的输出组的指针。

 项目必须为其支持的每个配置返回相同数量的组，即使组中包含的输出数可能因配置而异。 从项目中的配置到配置，组还必须具有相同的标识符信息（规范名称、显示名称和组信息）。 有关详细信息，请参阅[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

 要启用调试，您的配置应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>。 `IVsDebuggableProjectCfg`是项目实现的可选接口，允许调试器启动配置，并在 配置对象上实现 ， `IVsCfg` `IVsProjectCfg` 当用户选择通过按 F5 启动调试器时，环境将调用它。

 `ISpecifyPropertyPages`并`IDispatch`结合属性页向用户检索和显示与配置相关的信息。 有关详细信息，请参阅[属性页](../../extensibility/internals/property-pages.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
- [属性页](../../extensibility/internals/property-pages.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
