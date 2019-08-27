---
title: 项目子设计 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62430521"
---
# <a name="project-subtypes-design"></a>项目子类型设计
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型允许 Vspackage 扩展基于 Microsoft Build Engine (MSBuild) 项目。 使用聚合可以重复使用托管的核心项目系统中实现的大容量[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]但仍然自定义用于特定方案的行为。  
  
 以下主题详细说明的基本设计和实现项目子类型：  
  
- 项目子类型设计。  
  
- 多级别聚合。  
  
- 支持接口。  
  
## <a name="project-subtype-design"></a>项目子类型设计  
 项目子类型的初始化通过聚合主<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>对象。 这种聚合将使项目子类型重写或增强的大多数功能的基础项目。 项目子类型获取处理所使用的属性的第一个机会<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>，使用的命令<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>并<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>，和项目项管理使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>。 此外可以扩展项目子类型：  
  
- 项目配置对象。  
  
- 依赖于配置的对象。  
  
- 配置独立于浏览对象。  
  
- 项目自动化对象。  
  
- 项目自动化属性集合。  
  
  通过项目子类型的可扩展性的详细信息，请参阅[属性和由项目子类型扩展方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)。  
  
##### <a name="policy-files"></a>策略文件  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]环境提供的扩展基项目系统与项目子类型在其实现中的策略文件示例。 策略文件允许的形成[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]通过管理功能，其中包括在解决方案资源管理器中，环境**添加项目**对话框中，**添加新项**对话框和**属性**对话框。 策略子类型重写并增强了这些功能通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>，`IOleCommandTarget`和<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>实现。  
  
##### <a name="aggregation-mechanism"></a>聚合机制  
 环境的项目子类型聚合机制支持多个级别的聚合，从而允许由进一步 flavoring 风格的项目来实现高级子类型。 此外，支持对象的一个项目子类型，如<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>，旨在允许多个级别的分层。 为了与 COM 和 COM 的限制保持一致聚合规则、 项目子类型和基项目需要以协作方式进行编程以使内部的子类型或基项目能够正确地参与委派方法调用，以及管理引用计数. 也就是说，要聚合的项目必须进行编程，以支持聚合。  
  
 下图显示了多级项目子类型聚合的示意表示形式。  
  
 ![Visual Studio 多级项目风格图](../../extensibility/internals/media/vs-multilevelprojectflavor.gif "VS_MultilevelProjectFlavor")  
多级项目子类型  
  
 多级项目子类型聚合包含三个级别，聚合由项目子类型，然后进一步聚合的高级的项目子类型的基本项目。 图重点介绍一些作为的一部分提供的支持接口[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]项目子类型体系结构。  
  
##### <a name="deployment-mechanisms"></a>部署机制  
 基本项目系统的许多项目子类型通过增强的功能，包括部署机制。 项目子类型通过实现配置接口影响部署机制 (如<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>并<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>) 由上调用 QueryInterface 检索<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>。 在项目子类型和高级的项目子类型在其中添加不同的配置的实现方案中，调用的基础项目`QueryInterface`上的高级的项目子类型`IUnknown`。 如果内部项目子类型包含配置实现的基础项目要求的高级的项目子类型委托给内部项目子类型提供的实现。 作为一种机制来持久保存到另一个状态从一个聚合级别，所有级别的项目子类型都实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>到项目文件将保存非生成相关的 XML 数据。 有关详细信息，请参阅[MSBuild 项目文件中保存数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)。 <xref:EnvDTE80.IInternalExtenderProvider> 作为一种机制来自动化扩展程序检索项目子类型实现。  
  
 下图重点介绍的自动化扩展程序实现中，项目配置浏览对象具体而言，项目子类型用于扩展基本项目系统。  
  
 ![图： VS 项目风格自动扩展程序](../../extensibility/internals/media/vs-projectflavorautoextender.gif "VS_ProjectFlavorAutoExtender")  
项目子类型自动化扩展程序。  
  
 项目子类型可以进一步扩展通过扩展自动化对象模型的基本项目系统。 这些定义为 DTE 自动化对象的一部分，并用于扩展项目对象`ProjectItem`对象和`Configuration`对象。 有关详细信息，请参阅[扩展基项目对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)。  
  
## <a name="multi-level-aggregation"></a>多级别的聚合  
 包装较低级别的项目子类型的项目子类型实现需要以协作方式进行编程以允许内部项目子类型，才能正常工作。 一系列编程职责包括：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>包装的内部的子类型的项目子类型的实现必须委托给<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>内部项目子类型的两个实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>方法。  
  
- <xref:EnvDTE80.IInternalExtenderProvider>包装项目子类型的实现必须委托给其内部项目子类型的。 具体而言，实现<xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A>需要从内部项目子类型获取名称的字符串，然后执行连接它想要添加为扩展程序的字符串。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>包装项目子类型的实现必须实例化<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>对象其内部项目子类型，然后将其保留为私有委托，因为仅基项目的项目配置对象直接知道包装器项目子类型配置对象存在。 外部项目子类型可以最初选择想要直接处理配置接口，然后委托给内部项目子类型实现的其余部分<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A>。  
  
## <a name="supporting-interfaces"></a>支持接口  
 基础项目调用委托给支持项目子类型，通过添加接口来扩展其实现的各个方面。 这包括扩展项目配置对象和各种属性浏览器对象。 这些接口通过调用检索`QueryInterface`上`punkOuter`(指向的`IUnknown`) 的最外层项目子类型聚合器。  
  
|接口|项目子类型|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|允许为项目子类型：<br /><br /> -提供的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>。<br />-项目子类型，以提供自己的实现，从而控制启动的调试器<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>。<br />-禁用通过适当地处理设计时表达式计算`DBGLAUNCH_DesignTimeExprEval`情况下，在其实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A>。|  
|<xref:EnvDTE80.IInternalExtenderProvider>|允许为项目子类型：<br /><br /> 扩展<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>的项目以添加或删除配置项目的独立属性。<br />扩展项目自动化对象 (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) 的项目。<br /><br /> 上面的属性值取自<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>枚举。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|允许项目子类型，若要将映射回<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>给定项目配置浏览对象的对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|允许项目子类型，若要将映射回<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>或`VSITEMID`给定项目配置浏览对象的对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|允许项目子类型，以任意结构化的 XML 将数据保存到项目文件 （.vbproj 或.csproj）。 此数据不是对 MSBuild 可见的。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|允许为项目子类型：<br /><br /> -添加新的 MSBuild 属性，以持久保存。<br />-从 MSBuild 中删除不必要的属性。<br />-查询的当前值为 MSBuild 属性。<br />-更改 MSBuild 属性的当前值。|  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
