---
title: 属性页 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a45e4a98326fe829b8f87a4ecfce669118cd9d0e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205781"
---
# <a name="property-pages"></a>属性页
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

用户可以使用属性页查看和更改与项目配置相关的属性和独立属性。 "属性 **页** " 按钮在 " **属性** " 窗口中或在为所选对象提供属性页视图的对象的解决方案资源管理器工具栏上启用。 属性页由环境创建，可用于解决方案和项目。 但是，它们也可以提供给使用依赖于配置的属性的项目项。 当项目中的文件需要不同的编译器开关设置才能正确生成时，可以使用此功能。  
  
## <a name="using-property-pages"></a>使用属性页  
 如果属性页已显示并且所选内容更改 (例如，从解决方案到项目) ，则页面中显示的信息将更改以显示新选择的属性。 如果对象上没有支持属性页的属性，则属性页为空。  
  
 如果选择了多个对象，则 "属性" 页将显示所有选定项的属性交集。 如果所选项目不包含依赖于配置的属性，并且单击解决方案资源管理器工具栏上的 " **属性页** " 按钮，则焦点将更改为属性窗口。 有关与属性窗口和选择相关的详细信息，请参阅 [扩展属性](../../extensibility/internals/extending-properties.md)。  
  
 如果为多个对象显示属性，并且在属性页上更改了某个值，则这些对象的所有值将设置为新值，即使它们最初是不同的，并且在显示单个对象的属性时该页为空白。  
  
 中提供了两种常规类型的 **ProjectProperty 页** 对话框 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 在第一种情况下，对于 Visual Basic 项目，例如，使用字段格式显示属性页，如以下屏幕截图所示。 在第二个（如本节后面所示）中，属性页承载的属性网格与 "属性" 窗口中找到的属性网格类似。  
  
 ![Visual Basic 属性页](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages")  
具有字段格式和树结构的 "项目属性页" 对话框  
  
 "属性页" 对话框中的树结构不是使用生成的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 环境（基于由传递给它的级别名称 <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> 接口）生成它。  
  
 属性页上只能有两个顶级类别 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ：  
  
- 通用属性，为所选对象显示独立于配置的信息。 因此，当选择某个通用属性子类别时，该对话框顶部的 "配置"、"平台" 和 "Configuration Manager" 选项将不可用。  
  
- 配置属性，其中包含与解决方案或项目的调试、优化和生成参数相关的依赖于配置的信息。  
  
  不能创建任何其他顶级类别，但可以选择不在的实现中显示其中一种 `IVsPropertyPage` 。 例如，如果没有要为对象显示的任何独立于配置的属性，则可以选择不显示 "通用属性" 类别。 如果在 `ISpecifyPropertyPages` `ISpecifyPropertyPages` 配置对象 (实现 `IVsCfg` 、 `IVsProjectCfg` 和相关接口) 的对象实现时，将显示从项的浏览对象和配置属性实现的公共属性。  
  
  顶级类别下显示的每个类别都表示一个单独的属性页。 对话框中可用的类别和子类别项由和的实现确定 `ISpecifyPropertyPages` `IVsPropertyPage` 。  
  
  `IDispatch` 选择容器中具有要在属性页上显示的属性的项的对象将实现 `ISpecifyPropertyPages` 以枚举类 id 列表。 类 Id 作为变量传递给 `ISpecifyPropertyPages` ，并用于实例化属性页。 类 Id 列表还会传递到 `IVsPropertyPage` ，以在对话框左侧创建树结构。 然后，属性页会将信息传递回 `IDispatch` 实现的对象， `ISpecifyPropertyPages` 并填充每个页面的信息。  
  
  使用 `IDispatch` 对选择容器中的每个对象使用来检索浏览对象的属性。  
  
  `Help::DisplayTopicFromF1Keyword`在 VSPackage 中实现可提供 "帮助" 按钮的功能。  
  
  有关详细信息，请 `IDispatch` 参阅 `ISpecifyPropertyPages` MSDN library 中的和。  
  
  示例中显示的第二种属性页类型为 "属性" 网格的窗体，如以下屏幕截图所示。  
  
  ![VC 属性页](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages")  
  "属性页" 对话框和 "属性" 网格  
  
  `IVSMDPropertyBrowser` `IVSMDPropertyGrid` 在 vsmanaged) 中声明的接口和 (用于在对话框或窗口中创建和填充 "属性" 网格。  
  
  项目的体系结构与以前版本的相比已发生显著变化 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 特别是，活动的项目的概念已发生更改。 在中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，没有活动项目的概念。 在以前的开发环境中，活动项目是生成和部署命令的项目将默认为，而不考虑上下文。 现在，解决方案控制和仲裁哪些生成和部署命令适用于哪些项目。  
  
  以前的活动项目现在是以三种不同方式之一捕获的：  
  
- 启动项目  
  
   你可以从解决方案的属性页中指定一个项目，当用户按 F5 或从 "生成" 菜单中选择 "运行" 时，将启动该项目。 这种方式的工作方式类似于旧的活动项目，其名称以粗体解决方案资源管理器显示。  
  
   可以通过调用将启动项目作为自动化模型中的属性进行检索 `DTE.Solution.SolutionBuild.StartupProjects` 。 在 VSPackage 中，可以调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> 方法。 `IVsSolutionBuildManager` SID_SVsSolutionBuildManager 上提供作为服务 `QueryService` 。 有关详细信息，请参阅 [项目配置对象](../../extensibility/internals/project-configuration-object.md) 和 [解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
- 活动解决方案生成配置  
  
   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 具有活动解决方案配置，可通过实现在自动化模型中使用 `DTE.Solution.SolutionBuild.ActiveConfiguration` 。 解决方案配置是一个集合，其中包含解决方案中每个项目的一个项目配置 (每个项目可以具有多个配置，多个平台上具有不同名称) 。 有关与解决方案的属性页相关的详细信息，请参阅 [解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
- 当前选择的项目  
  
   实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> 方法以检索项目层次结构和项目项或选定的项。 从 DTE，你可以使用 `SelectedItems.SelectedItem.Project` 和 `SelectedItems.SelectedItem.ProjectItem` 方法。 核心文档中的标题下有示例代码 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>   
 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)   
 [项目配置对象](../../extensibility/internals/project-configuration-object.md)   
 [解决方案配置](../../extensibility/internals/solution-configuration.md)
