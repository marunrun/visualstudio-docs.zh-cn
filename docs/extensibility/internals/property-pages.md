---
title: 属性页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51487b35686da9676f201a157ddb8e47afb75ce8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725061"
---
# <a name="property-pages"></a>属性页
用户可以使用属性页查看和更改与项目配置相关的属性和独立属性。 "属性**页**" 按钮在 "**属性**" 窗口中或在为所选对象提供属性页视图的对象的解决方案资源管理器工具栏上启用。 属性页由环境创建，可用于解决方案和项目。 但是，它们也可以提供给使用依赖于配置的属性的项目项。 当项目中的文件需要不同的编译器开关设置才能正确生成时，可以使用此功能。

## <a name="using-property-pages"></a>使用属性页
 如果属性页已显示并且所选内容（例如，从解决方案到项目）发生更改，则页面中显示的信息将更改以显示新选择的属性。 如果对象上没有支持属性页的属性，则属性页为空。

 如果选择了多个对象，则 "属性" 页将显示所有选定项的属性交集。 如果所选项目不包含依赖于配置的属性，并且单击解决方案资源管理器工具栏上的 "**属性页**" 按钮，则焦点将更改为属性窗口。 有关与属性窗口和选择相关的详细信息，请参阅[扩展属性](../../extensibility/internals/extending-properties.md)。

 如果为多个对象显示属性，并且在属性页上更改了某个值，则这些对象的所有值将设置为新值，即使它们最初是不同的，并且在显示单个对象的属性时该页为空白。

 @No__t_1 中提供了两种常规类型的 " **ProjectProperty 页**" 对话框。 在第一种情况下，对于 Visual Basic 项目，例如，使用字段格式显示属性页，如以下屏幕截图所示。 在第二个（如本节后面所示）中，属性页承载的属性网格与 "属性" 窗口中找到的属性网格类似。

 ![Visual Basic 属性页](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages")具有字段格式和树结构的 "项目属性页" 对话框

 "属性页" 对话框中的树结构不是使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 生成的。 根据 <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> 接口传递给它的级别名称，环境将生成该环境。

 @No__t_0 属性页面上仅提供两个顶级类别：

- 通用属性，为所选对象显示独立于配置的信息。 因此，当选择某个通用属性子类别时，该对话框顶部的 "配置"、"平台" 和 "Configuration Manager" 选项将不可用。

- 配置属性，其中包含与解决方案或项目的调试、优化和生成参数相关的依赖于配置的信息。

  您无法创建任何其他顶级类别，但您可以选择不在 `IVsPropertyPage` 的实现中显示其中一种类别。 例如，如果没有要为对象显示的任何独立于配置的属性，则可以选择不显示 "通用属性" 类别。 @No__t_0 如果在配置对象（实现 `IVsCfg`、`IVsProjectCfg` 和相关接口的对象）中实现 `ISpecifyPropertyPages`，则将显示从项的浏览对象和配置属性实现的公共属性。

  顶级类别下显示的每个类别都表示一个单独的属性页。 对话框中可用的类别和子类别项由 `ISpecifyPropertyPages` 和 `IVsPropertyPage` 的实现确定。

  选择容器中具有要在属性页上显示的属性的项 `IDispatch` 对象将实现 `ISpecifyPropertyPages` 来枚举类 Id 列表。 类 Id 作为变量传递给 `ISpecifyPropertyPages`，并用于实例化属性页。 类 Id 列表还会传递到 `IVsPropertyPage`，以在对话框左侧创建树结构。 然后，属性页会将信息传递回实现 `ISpecifyPropertyPages` 的 `IDispatch` 对象，并填充每个页的信息。

  使用选择容器中每个对象的 `IDispatch` 检索浏览对象的属性。

  在 VSPackage 中实现 `Help::DisplayTopicFromF1Keyword` 提供 "帮助" 按钮的功能。

  有关详细信息，请参阅 MSDN library `IDispatch` 和 `ISpecifyPropertyPages`in。

  示例中显示的第二种属性页类型为 "属性" 网格的窗体，如以下屏幕截图所示。

  ![VC 属性页](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages")"属性页" 对话框和 "属性" 网格

  @No__t_0 和 `IVSMDPropertyGrid` （在 vsmanaged 中声明）的接口用于创建和填充对话框或窗口中的 "属性" 网格。

  项目的体系结构在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的过去版本中发生了显著变化。 特别是，活动的项目的概念已发生更改。 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中，没有活动项目的概念。 在以前的开发环境中，活动项目是生成和部署命令的项目将默认为，而不考虑上下文。 现在，解决方案控制和仲裁哪些生成和部署命令适用于哪些项目。

  以前的活动项目现在是以三种不同方式之一捕获的：

- 启动项目

   你可以从解决方案的属性页中指定一个项目，当用户按 F5 或从 "生成" 菜单中选择 "运行" 时，将启动该项目。 这种方式的工作方式类似于旧的活动项目，其名称以粗体解决方案资源管理器显示。

   可以通过调用 `DTE.Solution.SolutionBuild.StartupProjects`，将启动项目作为自动化模型中的属性进行检索。 在 VSPackage 中，可以调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> 方法。 `IVsSolutionBuildManager` 在 SID_SVsSolutionBuildManager 上可 `QueryService` 为服务。 有关详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)和[解决方案配置](../../extensibility/internals/solution-configuration.md)。

- 活动解决方案生成配置

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 具有活动解决方案配置，可通过实现 `DTE.Solution.SolutionBuild.ActiveConfiguration` 在自动化模型中提供。 解决方案配置是一个集合，该集合包含解决方案中每个项目的一个项目配置（每个项目可以在多个平台上具有多个具有不同名称的配置）。 有关与解决方案的属性页相关的详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

- 当前选择的项目

   实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> 方法来检索项目层次结构和项目项，或选定项。 从 DTE，你将使用 `SelectedItems.SelectedItem.Project` 和 `SelectedItems.SelectedItem.ProjectItem` 方法。 核心 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 文档中的标题下有示例代码。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)