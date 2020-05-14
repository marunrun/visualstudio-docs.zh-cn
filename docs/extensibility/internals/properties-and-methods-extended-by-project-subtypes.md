---
title: 按项目子类型扩展的属性和方法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9963f779055fcf1ed0efd8c47abbe1cce35631a6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706198"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>项目子类型扩展的属性和方法
项目子类型具有很大的力量来影响项目的行为，因为它是作为基础项目的聚合器构造的。 本节总结了一些可以通过项目子类型进行增强或修改的功能。

## <a name="features-gained-by-aggregation"></a>通过聚合获取的功能
 下表总结了聚合使项目子类型能够在基础项目中重写的许多方法。

|被聚合覆盖的方法|项目子类型|
|---------------------------------------|---------------------|
|从<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|使项目子类型<br /><br /> - 更改项目节点的标题和图标。<br />- 完全覆盖`Browse`项目对象。<br />- 控制是否可以重命名项目。<br />- 控制排序顺序。<br />- 控制动态帮助的用户上下文。|
|从<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|使项目子类型能够控制向设计人员和编辑器提供的上下文服务。|
|从<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>：<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|使项目子类型<br /><br /> - 参与项目命令的命令路由。<br />- 添加、删除或禁用项目环境命令和解决方案资源管理器活动命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|使项目子类型能够筛选用户在"**添加新项目"** 对话框中看到的内容。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|使项目子类型<br /><br /> - 确定给定文件扩展名的默认生成器。<br />- 将人可读生成器名称映射到 COM 对象。|

## <a name="properties-used-by-project-subtypes"></a>项目子类型使用的属性
 环境和基础项目系统可以使用下表中详细属性<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID>和<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>枚举，使项目子类型能够控制项目系统的各种功能。

|VSHPROPID 属性|项目子类型|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|允许项目子类型控制 **"添加项目"** 对话框的内容。 项目子类型可以提供模板目录的新规范、添加新类型的项、删除现有项以及重新组织基础项目"**添加项目"** 对话框中的项子集。|
|`PropertyPagesCLSIDList`|允许项目子类型添加或删除与配置无关的属性页。|
|`CfgPropertyPagesCLSIDList`|允许项目子类型添加或删除与配置相关的属性页。|
|`ExtObjectCATID`|允许项目子类型通过了解扩展器 CATID 为项目或项目项对象提供自动化扩展器。 例如，项目子类型可以提供自定义`Project.Extender("<subtype>")`对象。|
|`BrowseObjectCATID`|允许项目子类型通过了解扩展器 CATID 为`Browse`对象提供自动化扩展器。 例如，项目子类型可以向<xref:EnvDTE.Project.Properties%2A>集合添加额外的属性。|
|`CfgBrowseObjectCATID`|允许项目子类型为项目配置浏览对象提供自动化扩展器。 例如，项目子类型可以向<xref:EnvDTE.Configuration.Properties%2A>集合添加额外的属性。|
|`CfgExtObjectCATID`|允许项目子类型为配置对象提供自动化扩展器。|
|`DefaultPlatformName`|允许项目子类型确定项目配置对象的平台名称。|

 基础项目提供上述属性的默认实现。 基础项目通过在最外层的项目`QueryInterface`子<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>类型上调用来获取这些，从而允许项目子类型覆盖属性的实现。

## <a name="see-also"></a>请参阅
- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)
