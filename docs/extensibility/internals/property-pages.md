---
title: 属性页 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ac788f51bcdc52cd39469a272909890333c5016b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706055"
---
# <a name="property-pages"></a>属性页
用户可以使用属性页查看和更改与项目配置无关的属性和 - 独立属性。 属性**页**按钮在 **"属性"** 窗口或解决方案资源管理器工具栏上为提供所选对象的属性页视图的对象启用。 属性页由环境创建，可用于解决方案和项目。 但是，它们也可以提供给使用与配置相关的属性的项目项。 当项目中的文件需要不同的编译器开关设置才能正确生成时，可能会使用此功能。

## <a name="using-property-pages"></a>使用属性页
 如果属性页已显示且所选内容发生更改（例如，从解决方案到项目），则页面中显示的信息将更改以显示新选择的属性。 如果对象上没有支持属性页的属性，则属性页为空。

 如果选择了多个对象，则属性页将显示所有选定项的属集。 如果所选项不包含与配置相关的属性，并且单击"解决方案资源管理器"工具栏上**的属性页**按钮，则对焦将更改为"属性"窗口。 有关属性窗口和选择的详细信息，请参阅[扩展属性](../../extensibility/internals/extending-properties.md)。

 如果为多个对象显示属性，并在属性页上更改值，则对象的所有值都设置为新值，即使它们最初不同，并且当显示单个对象的属性时页面为空也是如此。

 中提供了两种常规类型的**项目属性页**对话框[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 例如，在第一个中，对于 Visual Basic 项目，属性页使用字段格式显示，如下图所示。 在第二部分（本节后面显示）中，属性页承载的属性网格与属性窗口中的属性网格类似。

 ![可视化基本属性页](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages")具有字段格式和树结构的项目属性页对话框

 属性页对话框中的树结构不是使用 构建的<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>。 环境基于 接口<xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages><xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>传递给它的级别名称，生成它。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]属性页上只有两个顶级类别可用：

- 公共属性，它显示所选对象或对象与配置无关的信息。 因此，当选择"通用属性"子类别之一时，对话框顶部的"配置、平台"和"配置管理器"选项不可用。

- 配置属性，其中包含与解决方案或项目的调试、优化和生成参数相关的配置信息。

  不能创建任何其他顶级类别，但可以选择在 的实现中不显示其中一`IVsPropertyPage`个类别。 例如，如果您没有任何与配置无关的属性要显示对象，则可以选择不显示"公共属性"类别。 在配置对象（对象`ISpecifyPropertyPages`实现`IVsCfg`）`IVsProjectCfg`和相关接口中实现时，如果从项目的浏览对象`ISpecifyPropertyPages`和配置属性实现，则显示公共属性。

  显示在顶级类别下的每个类别表示单独的属性页。 对话框中可用的类别和子类别条目由 和`ISpecifyPropertyPages``IVsPropertyPage`的实现确定。

  `IDispatch`选择容器中具有要在属性页上显示的属性的对象，以`ISpecifyPropertyPages`枚举类 I 的清单。 类 I 以变量传递到`ISpecifyPropertyPages`，并用于实例化属性页。 类指示列表也会传递给，`IVsPropertyPage`以创建对话框左侧的树结构。 然后，属性页将信息传递回实现`IDispatch``ISpecifyPropertyPages`并填充每个页面的信息的对象。

  使用`IDispatch`选择容器中的每个对象检索浏览对象的属性。

  在`Help::DisplayTopicFromF1Keyword`VSPackage 中实现为"帮助"按钮提供了功能。

  有关详细信息，请参阅`IDispatch`MSDN`ISpecifyPropertyPages`库中和。

  示例中显示的第二种属性页承载属性网格的形式，如下图所示。

  ![VC 属性页](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages")属性页对话框，包含属性网格

  接口`IVSMDPropertyBrowser`和`IVSMDPropertyGrid`（在 vs 托管.h 中声明）用于在对话框或窗口中创建和填充属性网格。

  与过去的版本相比，项目的体系结构已经发生了很大变化[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 特别是，哪个项目处于活动状态的概念已经改变。 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中，没有活动项目的概念。 在以前的开发环境中，活动项目是生成和部署命令的项目，无论上下文如何，都默认为 。 现在，解决方案控制和仲裁生成和部署命令适用于哪些项目。

  以前处于活动状态的项目现在以三种不同方式之一捕获：

- 启动项目

   您可以从解决方案的属性页指定项目或项目，当用户按 F5 或从"生成"菜单中选择"运行"时，该项目将启动该项目或项目。 其工作方式与旧活动项目类似，其名称以粗体显示在解决方案资源管理器中。

   您可以通过调用`DTE.Solution.SolutionBuild.StartupProjects`来检索启动项目作为自动化模型中的属性。 在 VSPackage 中，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A>方法。 `IVsSolutionBuildManager`可在SID_SVsSolutionBuildManager`QueryService`作为服务提供。 有关详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)和[解决方案配置](../../extensibility/internals/solution-configuration.md)。

- 活动解决方案生成配置

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]具有活动解决方案配置，可通过实现`DTE.Solution.SolutionBuild.ActiveConfiguration`在自动化模型中提供。 解决方案配置是一个集合，其中包含解决方案中每个项目的一个项目配置（每个项目可以在多个平台上具有多个配置，名称不同）。 有关解决方案属性页的详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

- 当前选定的项目

   实现方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A>以检索项目层次结构和项目项或所选项。 在 DTE 中，您将`SelectedItems.SelectedItem.Project`使用`SelectedItems.SelectedItem.ProjectItem`和 方法。 核心[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]文档中这些标题下有示例代码。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
