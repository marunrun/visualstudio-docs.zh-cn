---
title: 通过项目子类型扩展属性和方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 20892d50afc529b410e8e0bdfa3c4b52fdc1b9b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154128"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>项目子类型扩展的属性和方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型都有很多电量将影响项目的行为，因为它的结构为基础的项目的聚合器。 本部分总结了一些功能可以增强或修改的项目子类型。  
  
## <a name="features-gained-by-aggregation"></a>聚合所获得的功能  
 下表总结了很多聚合使项目子类型基项目中重写的方法。  
  
|通过聚合中被重写的方法|项目子类型|  
|---------------------------------------|---------------------|  
|从<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|启用对项目子类型<br /><br /> -更改的标题和图标的项目节点。<br />-完全重写项目`Browse`对象。<br />-控制是否可以重命名项目。<br />控制排序顺序。<br />动态帮助控制用户上下文。|  
|从<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|使项目子类型来控制哪些上下文服务提供给设计器和编辑器。|  
|从<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|启用对项目子类型<br /><br /> -参与项目命令的命令路由。<br />-添加、 删除或禁用项目环境命令和解决方案资源管理器活动命令。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|使项目子类型，以筛选用户中看到的内容**添加新项**对话框。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|启用对项目子类型<br /><br /> -确定默认生成器提供的文件扩展名。<br />-将的人工可读的生成器名称映射到 COM 对象。|  
  
## <a name="properties-used-by-project-subtypes"></a>使用项目子类型的属性  
 环境和基本项目系统可以使用中的属性<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID>和<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>下表中的详细若要启用项目子类型，用于控制各种功能的项目系统的枚举。  
  
|VSHPROPID 属性|项目子类型|  
|------------------------|---------------------|  
|`AddItemTemplatesGuid`|允许项目子类型来控制的内容**添加项**对话框。 项目子类型可以提供模板目录的新规范，添加新项的类型，删除现有项，并重新组织的基础项目中的项的子集**添加项**对话框。|  
|`PropertyPagesCLSIDList`|允许项目子类型以添加或删除独立于配置的属性页。|  
|`CfgPropertyPagesCLSIDList`|允许项目子类型以添加或删除依赖于配置的属性页。|  
|`ExtObjectCATID`|允许项目子类型来提供自动化扩展程序的项目或项目项对象通过了解扩展程序 CATID。 例如，项目子类型可以提供自定义`Project.Extender("<subtype>")`对象。|  
|`BrowseObjectCATID`|允许项目子类型提供的自动化扩展程序`Browse`通过了解扩展程序 CATID 的对象。 例如，项目子类型可以额外将属性添加到<xref:EnvDTE.Project.Properties%2A>集合。|  
|`CfgBrowseObjectCATID`|允许项目子类型为项目配置浏览对象提供自动化扩展程序。 例如，项目子类型可以额外将属性添加到<xref:EnvDTE.Configuration.Properties%2A>集合。|  
|`CfgExtObjectCATID`|允许项目子类型为配置对象提供自动化扩展程序。|  
|`DefaultPlatformName`|允许项目子类型来确定项目的配置对象的平台名称。|  
  
 基本项目提供了以上属性的默认实现。 基础项目获取通过调用这些`QueryInterface`为<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>上最外面的项目子类型，从而允许重写属性实现的项目子类型。  
  
## <a name="see-also"></a>请参阅  
 [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)
