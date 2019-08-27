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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205781"
---
# <a name="property-pages"></a>属性页
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

用户可以查看和更改项目依赖于配置和-独立属性使用属性页。 一个**属性页**中启用按钮**属性**窗口或对象，它提供所选对象的属性页面视图的解决方案资源管理器工具栏上。 属性页创建的环境，并可用于解决方案和项目。 它们，但是，也可以是可进行的项目项使用的配置相关的属性。 在项目中的文件需要不同的编译器开关设置才能正确生成时，可能会使用此功能。  
  
## <a name="using-property-pages"></a>使用属性页  
 如果尚未显示属性页，并且所选内容更改 （例如，从向项目解决方案） 页更改为显示新选择的属性中显示的信息。 如果没有在对象上支持属性页的属性，属性页为空。  
  
 如果选择了多个对象，属性页将显示所有选定的项目的属性的交集。 如果所选的项目不包含依赖于配置的属性和**属性页**单击解决方案资源管理器工具栏上的按钮时，焦点更改到属性窗口。 与属性窗口和所选内容相关的详细信息，请参阅[扩展属性](../../extensibility/internals/extending-properties.md)。  
  
 如果属性都显示为多个对象，更改属性页中的值，所有的对象的值将设置为新值中，即使它们是最初不同的页面是保留为空时显示的各个对象的属性。  
  
 有两种常规类型的**ProjectProperty 页面**对话框中提供[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 在第一个 Visual Basic 项目，例如，属性页使用显示的字段格式，如以下屏幕截图中所示。 在第二个，稍后在本部分中，该属性页上的主机属性网格类似于在属性窗口中找到的。  
  
 ![Visual Basic 属性页](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages")  
字段格式和树的结构与项目属性页对话框  
  
 在属性页对话框中的树状结构不使用生成<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>。 在环境中，根据传递给它的级别名称<xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>接口，生成它。  
  
 有只有两个顶级类别可在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]属性页：  
  
- 通用属性，将显示所选的对象或对象的独立于配置的信息。 因此，选中一个通用属性子类别后，在对话框顶部的配置、 平台和配置管理器选项不可用。  
  
- 配置属性，其中包含与解决方案或项目的调试、 优化和生成参数相关的配置相关信息。  
  
  无法创建任何其他的顶级类别，但可以选择不希望显示的实现中的一个或另一个`IVsPropertyPage`。 如果，例如，你没有要显示的对象的任何独立于配置的属性，您可以选择不希望显示的通用属性类别。 如果显示通用属性`ISpecifyPropertyPages`实现时，从项的浏览对象和配置属性实现`ISpecifyPropertyPages`中的配置对象 (对象实现`IVsCfg`， `IVsProjectCfg`，及相关接口）。  
  
  每个类别成为顶级类别下显示表示单独的属性页。 类别和子类别可用项对话框中的由实现`ISpecifyPropertyPages`和`IVsPropertyPage`。  
  
  `IDispatch` 选择容器中的某些项具有属性显示在属性页实现的对象`ISpecifyPropertyPages`枚举类 Id 的列表。 类 Id 作为变量传递到`ISpecifyPropertyPages`和用于实例化的属性页。 类 Id 的列表也将传递到`IVsPropertyPage`创建对话框的左侧的树状结构。 然后，此属性页的信息传递回`IDispatch`对象，它实现`ISpecifyPropertyPages`和填充的每个页的信息。  
  
  使用浏览对象的属性进行检索`IDispatch`选择容器中每个对象。  
  
  实现`Help::DisplayTopicFromF1Keyword`中你的 VSPackage 提供的功能的帮助按钮。  
  
  有关详细信息，请参阅`IDispatch`和`ISpecifyPropertyPages`MSDN 库中。  
  
  第二个属性页中显示的类型的示例主机窗体的属性网格中，如以下屏幕截图中所示。  
  
  ![VC 属性设置页面](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages")  
  使用属性网格属性页对话框  
  
  接口`IVSMDPropertyBrowser`和`IVSMDPropertyGrid`（vsmanaged.h 中声明） 用于创建和填充属性网格中的对话框或窗口。  
  
  从以前版本的项目的体系结构发生了显著[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 具体而言，这一概念的哪个项目处于活动状态已更改。 在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，不存在某个活动项目的概念。 在上一个开发环境中，活动的项目是项目的生成和部署命令而不考虑上下文会默认为。 现在，解决方案控制并进行仲裁的生成和部署命令将应用于哪些项目。  
  
  现在，在某个三种不同方式中捕获什么以前是活动项目：  
  
- 启动项目  
  
   您可以指定一个项目或从解决方案的属性页中，当用户按下 F5 或从生成菜单中选择运行时将启动项目。 这的工作方式类似于意义上说，使用加粗字体其名称显示在解决方案资源管理器中的旧活动项目。  
  
   通过调用检索自动化模型中的属性作为启动项目`DTE.Solution.SolutionBuild.StartupProjects`。 在 VSPackage 中，可以调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A>方法。 `IVsSolutionBuildManager` 作为服务通过提供`QueryService`SID_SVsSolutionBuildManager 上。 有关详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)并[解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
- 活动解决方案生成配置  
  
   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 具有活动解决方案配置，可通过实现自动化模型中`DTE.Solution.SolutionBuild.ActiveConfiguration`。 解决方案配置是包含一个项目配置的解决方案 （每个项目可以具有不同名称的多个平台有多个配置） 中的每个项目集合。 与解决方案的属性页的详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
- 当前选定项目  
  
   实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A>方法来检索其中的项目层次结构和项目项或所选的项。 从 DTE，您将使用`SelectedItems.SelectedItem.Project`和`SelectedItems.SelectedItem.ProjectItem`方法。 在这些核心中的标题下的示例代码[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]文档。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>   
 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)   
 [项目配置对象](../../extensibility/internals/project-configuration-object.md)   
 [解决方案配置](../../extensibility/internals/solution-configuration.md)
