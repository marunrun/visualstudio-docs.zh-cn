---
title: 项目配置对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 32e4d34ec3d1fbe8753b4185cab76caa77038bd1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434835"
---
# <a name="project-configuration-object"></a>项目配置对象
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目配置对象管理到 UI 的配置信息的显示。  
  
 ![Visual Studio 项目配置](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg")  
项目配置属性页  
  
 项目配置提供程序管理的项目配置。 在环境和其他包，才能访问和检索有关项目的配置的信息，请调用附加到项目的配置提供程序对象的接口。  
  
> [!NOTE]
> 无法创建或以编程方式编辑解决方案配置文件。 必须使用`DTE.SolutionBuilder`。 请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)有关详细信息。  
  
 若要发布的配置 UI 中使用的显示名称，你的项目应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A>。 环境调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>，这会返回一系列`IVsCfg`可用于获取要在环境的用户界面中列出的配置和平台信息的显示名称的指针。 由存储在活动解决方案配置的项目的配置确定的活动配置和平台。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A>方法可以用于检索活动项目配置。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>对象可以选择在上实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper>对象，以允许您检索`IVsProjectCfg2`对象基于规范的项目配置名称。  
  
 另一种方法提供对项目配置访问权限的环境和其他项目的项目提供的一个实现，为`IVsCfgProvider2::GetCfgs`方法以返回一个或多个配置对象。 项目还可能会实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>，后者又继承`IVsProjectCfg`，从而从`IVsCfg`，以提供特定于配置的信息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 添加、 删除和重命名项目配置为支持平台和功能。  
  
> [!NOTE]
> 由于 Visual Studio 不再限制为两种配置类型、 处理配置的代码编写，不应使用的假设有关多个配置，也不应它编写时会假定，只有一个项目调试或零售，一定是配置。 这样，使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A>已过时。  
  
 调用`QueryInterface`从返回的对象上`IVsGetCfgProvider::GetCfgProvider`检索`IVsCfgProvider2`。 如果`IVsGetCfgProvider`通过调用找不到`QueryInterface`上`IVsProject3`项目对象，可以通过调用访问的配置提供程序对象`QueryInterface`为返回的对象的层次结构根浏览器对象上`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)`，或通过指向返回的配置提供程序的`IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)`。  
  
 `IVsProjectCfg2` 主要提供访问来生成、 调试和部署管理对象，并允许到组的输出可以自由的项目。 方法`IVsProjectCfg`并`IVsProjectCfg2`可用于实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>来管理生成过程中，和<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup>配置的输出组的指针。  
  
 项目必须返回相同数量的它支持即使的组中包含的输出数可能会有所不同 configuration 配置每个配置的组。 组还必须具有相同的标识符信息 （规范名称、 显示名称和组信息） 配置配置项目中。 有关详细信息，请参阅[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)。  
  
 若要启用调试，你的配置应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>。 `IVsDebuggableProjectCfg` 是实现以允许调试器以启动配置项目的可选接口，并且在配置对象上实现`IVsCfg`和`IVsProjectCfg`。 环境在用户选择通过按 F5 启动调试器时调用它。  
  
 `ISpecifyPropertyPages` 和`IDispatch`用属性页结合使用来检索并向用户显示依赖于配置的信息。 有关详细信息，请参阅[属性页](../../extensibility/internals/property-pages.md)。  
  
## <a name="see-also"></a>请参阅  
 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)   
 [用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)   
 [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)   
 [属性页](../../extensibility/internals/property-pages.md)   
 [解决方案配置](../../extensibility/internals/solution-configuration.md)
