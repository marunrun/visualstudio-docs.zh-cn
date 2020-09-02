---
title: 项目子类型设计 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0e7cd96324e5a2bbd6c9b0acf4125bc0450cfd06
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62430521"
---
# <a name="project-subtypes-design"></a>项目子类型设计
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型让 Vspackage 根据 Microsoft 生成引擎 (MSBuild) 扩展项目。 使用聚合可让你重复使用在中实现的核心托管项目系统， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 但仍会自定义特定方案的行为。  
  
 以下主题详细介绍了项目子类型的基本设计和实现：  
  
- 项目子类型设计。  
  
- 多级别聚合。  
  
- 支持接口。  
  
## <a name="project-subtype-design"></a>项目子类型设计  
 项目子类型的初始化通过聚合主 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 对象和对象实现。 此聚合使项目子类型可以重写或增强基本项目的大部分功能。 项目子类型通过使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 和的命令以及使用的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 项目项管理，获得处理属性的第一种机会 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> 。 项目子类型还可以扩展：  
  
- 项目配置对象。  
  
- 依赖于配置的对象。  
  
- 独立于配置的浏览对象。  
  
- 项目自动化对象。  
  
- 项目自动化属性集合。  
  
  有关项目子类型的扩展性的详细信息，请参阅 [按项目子类型扩展的属性和方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)。  
  
##### <a name="policy-files"></a>策略文件  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]环境提供一个示例，该示例在其策略文件的实现中扩展基本项目系统的项目子类型。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]通过管理包含 "解决方案资源管理器、"**添加项目**"对话框、"**添加新项**"对话框和"**属性**"对话框的功能，策略文件允许环境的整形。 策略子类型通过和实现覆盖和增强了这些功能 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> `IOleCommandTarget` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 。  
  
##### <a name="aggregation-mechanism"></a>聚合机制  
 环境的项目子类型聚合机制支持多个级别的聚合，从而允许通过 flavoring 风格项目进一步实现高级子类型。 另外，项目子类型的支持对象（例如 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> ）旨在允许分层的多个级别。 为了保持 COM 和 COM 聚合规则的约束，需要以协作方式对项目子类型和基本项目进行编程，以使内部子类型或基本项目能够正确参与委托方法调用和管理引用计数。 也就是说，必须对要聚合的项目进行编程以支持聚合。  
  
 下图显示了多级别项目子类型聚合的示意图表示。  
  
 ![图：Visual Studio 多级项目风格](../../extensibility/internals/media/vs-multilevelprojectflavor.gif "VS_MultilevelProjectFlavor")  
多级项目子类型  
  
 多级别项目子类型聚合由三个级别组成，这是一个由项目子类型聚合的基本项目，然后由高级项目子类型进一步聚合。 该图重点介绍作为 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 项目子类型体系结构一部分提供的一些支持接口。  
  
##### <a name="deployment-mechanisms"></a>部署机制  
 许多由项目子类型增强的基本项目系统功能是部署机制。 项目子类型通过实现 (（例如） <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>) （通过在上调用 QueryInterface 来检索）来影响部署机制 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> 。 在项目子类型和高级项目子类型添加不同配置实现的方案中，基本项目会对 `QueryInterface` 高级项目子类型的进行调用 `IUnknown` 。 如果内部项目子类型包含基本项目正在请求的配置实现，则高级项目子类型将委托给内部项目子类型提供的实现。 作为将状态从一个聚合级别保存到另一个聚合级别的机制，项目子类型的所有级别都实现， <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 以将与非生成相关的 XML 数据保存到项目文件中。 有关详细信息，请参阅 [在 MSBuild 项目文件中保留数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)。 <xref:EnvDTE80.IInternalExtenderProvider> 实现为从项目子类型检索自动化扩展程序的机制。  
  
 下图重点介绍自动化扩展器实现，特定于项目配置的浏览对象，由项目子类型用来扩展基本项目系统。  
  
 ![图：VS 项目风格自动扩展程序](../../extensibility/internals/media/vs-projectflavorautoextender.gif "VS_ProjectFlavorAutoExtender")  
项目子类型自动化扩展程序。  
  
 项目子类型可以通过扩展自动化对象模型进一步扩展基本项目系统。 它们定义为 DTE 自动化对象的一部分，并用于扩展项目对象、 `ProjectItem` 对象和 `Configuration` 对象。 有关详细信息，请参阅 [扩展基项目的对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)。  
  
## <a name="multi-level-aggregation"></a>多级别聚合  
 要使内部项目子类型正常工作，需要以协作方式对包装较低级别项目子类型的项目子类型实现进行编程。 编程职责的列表包括：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>包装内部子类型的项目子类型的实现必须委托给 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 和方法的内部项目子类型的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> 。  
  
- <xref:EnvDTE80.IInternalExtenderProvider>包装项目子类型的实现必须委托给其内部项目子类型的实现。 具体而言，实现 <xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> 需要从内部项目子类型获取名称的字符串，然后将它要添加的字符串连接到要添加为扩展程序的字符串。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>包装项目子类型的实现必须实例化 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> 其内部项目子类型的对象并将其保存为私有委托，因为只有基项目的项目配置对象直接知道包装项目子类型配置对象存在。 外部项目子类型最初可以选择要直接处理的配置接口，然后将其余的委托委托给内部项目子类型的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A> 。  
  
## <a name="supporting-interfaces"></a>支持接口  
 基本项目将调用委托给由项目子类型添加的支持接口，以扩展其实现的各个方面。 这包括扩展项目配置对象和各种属性浏览器对象。 通过 `QueryInterface` 在 `punkOuter` (指向 `IUnknown` 最外面的项目子类型聚合器的) 的指针来检索这些接口。  
  
|接口|项目子类型|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|允许项目子类型执行以下操作：<br /><br /> -提供的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 。<br />-通过允许项目子类型提供自己的实现来控制调试器的启动 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> 。<br />-通过 `DBGLAUNCH_DesignTimeExprEval` 在其实现中适当处理事例来禁用设计时表达式计算 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A> 。|  
|<xref:EnvDTE80.IInternalExtenderProvider>|允许项目子类型执行以下操作：<br /><br /> -扩展项目的， <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 以添加或删除项目的独立于配置的属性。<br />-将项目自动化对象 (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) 扩展。<br /><br /> 上面的属性值取自 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> 枚举。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|允许项目子类型映射回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> 给定的项目配置浏览对象的对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> `VSITEMID` 给定项目配置浏览对象的情况下，允许项目子类型映射回或对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|允许项目子类型将任意 XML 结构化数据保存到项目文件中， ( .vbproj 或 .csproj) 。 此数据对 MSBuild 不可见。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|允许项目子类型执行以下操作：<br /><br /> -添加要保存的新的 MSBuild 属性。<br />-从 MSBuild 中删除不必要的属性。<br />-查询 MSBuild 属性的当前值。<br />-更改 MSBuild 属性的当前值。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
