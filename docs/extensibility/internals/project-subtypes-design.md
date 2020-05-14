---
title: 项目子类型设计 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b939d197bfd7e58b555ca7698f08643e3d38ef2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706446"
---
# <a name="project-subtypes-design"></a>项目子类型设计

项目子类型允许 VS 包基于 Microsoft 构建引擎 （MSBuild） 扩展项目。 使用聚合可以重用在中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实现的大部分核心托管项目系统，但仍为特定方案自定义行为。

 以下主题详细介绍了项目子类型的基本设计和实现：

- 项目子类型设计。

- 多级聚合。

- 支持接口。

## <a name="project-subtype-design"></a>项目子类型设计

通过聚合主<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>类型和<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>对象来实现项目子类型的初始化。 此聚合使项目子类型能够覆盖或增强基础项目的大部分功能。 项目子类型获得使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>处理 属性的第一次机会，使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget><xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>和 命令 使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>和 和 以及 使用 项目项管理。 项目子类型还可以扩展：

- 项目配置对象。

- 与配置相关的对象。

- 与配置无关的浏览对象。

- 项目自动化对象。

- 项目自动化属性集合。

有关按项目子类型扩展的详细信息，请参阅[按项目子类型扩展的属性和方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)。

### <a name="policy-files"></a>策略文件

该[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境提供了一个示例，在策略文件实现中使用项目子类型扩展基础项目系统。 策略文件通过管理包括解决方案资源管理器、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**添加项目**对话框、**添加新项目**对话框和 **"属性"** 对话框的功能，允许塑造环境。 策略子类型通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>重写和增强这些功能，并通过`IOleCommandTarget`和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>实现。

### <a name="aggregation-mechanism"></a>聚合机制

环境的项目子类型聚合机制支持多个级别的聚合，从而允许通过进一步调味项目实现高级子类型。 此外，项目子类型的支持对象（如<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>）旨在允许多层分层。 为了符合 COM 和 COM 聚合规则的约束，需要协同编程项目子类型和基础项目，以使内部子类型或基础项目能够正确参与委派方法调用和管理引用计数。 也就是说，要聚合的项目必须编程以支持聚合。

下图显示了多级项目子类型聚合的原理图表示形式。

![图：Visual Studio 多级项目风格](../../extensibility/internals/media/vs_multilevelprojectflavor.gif)

多级项目子类型聚合由三个级别组成，一个基础项目，由项目子类型聚合，然后由高级项目子类型进一步聚合。 该图重点介绍了作为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目子类型体系结构的一部分提供的一些支持接口。

### <a name="deployment-mechanisms"></a>部署机制

项目子类型增强的许多基础项目系统功能包括部署机制。 项目子类型通过实现通过调用 上的<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg><xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>QueryInterface 检索的配置接口（如 和 ） 来影响部署机制。 在项目子类型和高级项目子类型都添加不同配置实现的情况下，基础项目调用`QueryInterface`高级项目子类型。 `IUnknown` 如果内部项目子类型包含基础项目要求的配置实现，则高级项目子类型将委托给内部项目子类型提供的实现。 作为一种将状态从一个聚合级别持久化到另一个聚合级别的机制，实现项目<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>子类型的所有级别都用于将非生成相关的 XML 数据保存到项目文件中。 有关详细信息，请参阅[MSBuild 项目文件中的持久数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)。 <xref:EnvDTE80.IInternalExtenderProvider>作为从项目子类型检索自动化扩展器的机制实现。

下图重点介绍了自动化扩展器实现，特别是项目配置浏览对象，项目子类型用于扩展基础项目系统。

![图：VS 项目风格自动扩展程序](../../extensibility/internals/media/vs_projectflavorautoextender.gif)

项目子类型可以通过扩展自动化对象模型进一步扩展基础项目系统。 这些被定义为 DTE 自动化对象的一部分，用于扩展 Project 对象、`ProjectItem`对象和`Configuration`对象。 有关详细信息，请参阅[扩展基础项目的对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)。

## <a name="multi-level-aggregation"></a>多级聚合

包装较低级别项目子类型的项目子类型实现需要协同编程，以使内部项目子类型正常运行。 编程职责列表包括：

- 包装<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>内部子类型的项目子类型的实现必须委托给内部项目子类型的<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>实现。两者<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>和方法。 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>

- 包装<xref:EnvDTE80.IInternalExtenderProvider>器子类型的实现必须委托给其内部项目子类型的实现。 特别是， 的<xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A>实现需要从内部项目子类型获取名称字符串，然后串联它要添加为扩展器的字符串。

- 包装<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>器项目子类型的实现必须实例化其内部项目子类型<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>的对象并将其作为私有委托保留，因为只有基础项目的项目配置对象直接知道包装器项目子类型配置对象存在。 外部项目子类型最初可以选择它要直接处理的<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A>配置接口，然后将其余部分委托给内部项目子类型的实现。

## <a name="supporting-interfaces"></a>支持接口

基本项目委托调用项目子类型添加的支持接口，以扩展其实现的各个方面。 这包括扩展项目配置对象和各种属性浏览器对象。 这些接口通过调用`QueryInterface`最外层项目`punkOuter`子类型聚合器的`IUnknown`（指向 的 指针） 来检索。

|接口|项目子类型|
|---------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|允许项目子类型：<br /><br /> - 提供 的<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>实现。<br />- 通过允许项目子类型提供其自己的实现来控制调试器的启动<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>。<br />- 禁用设计时表达式评估，`DBGLAUNCH_DesignTimeExprEval`在 实施 时适当处理案例<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A>。|
|<xref:EnvDTE80.IInternalExtenderProvider>|允许项目子类型：<br /><br /> - 扩展<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>项目的，以添加或删除项目的配置独立属性。<br />- 扩展项目的项目自动化对象<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtObject>（ ） 。<br /><br /> 上面的属性值取自<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>枚举。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|允许项目子类型映射回给定项目配置浏览<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>对象的对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|允许项目子类型映射回<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>或`VSITEMID`对象，给定项目配置浏览对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|允许项目子类型将任意 XML 结构化数据保存到项目文件 （.vbproj 或 .csproj）。 此数据对 MSBuild 不可见。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|允许项目子类型：<br /><br /> - 添加新的 MSBuild 属性以持久化。<br />- 从 MSBuild 中删除不必要的属性。<br />- 查询 MSBuild 属性的当前值。<br />- 更改 MSBuild 属性的当前值。|

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
