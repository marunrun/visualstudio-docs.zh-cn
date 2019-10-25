---
title: 按项目子类型扩展的属性和方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f5f67ac70b7ca6d5151a9115f20be88f6984d52
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725347"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>项目子类型扩展的属性和方法
项目子类型有很大的影响，因为它被构造为基本项目的聚合器。 本部分总结了项目子类型可以增强或修改的一些功能。

## <a name="features-gained-by-aggregation"></a>聚合获取的功能
 下表汇总了许多聚合使项目子类型在基本项目中重写的方法。

|聚合重写的方法|项目子类型|
|---------------------------------------|---------------------|
|从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|使项目子类型成为<br /><br /> -更改项目节点的标题和图标。<br />-完全重写 project `Browse` 对象。<br />-控制是否可以重命名项目。<br />-控制排序顺序。<br />-控制动态帮助的用户上下文。|
|从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>：<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|启用项目子类型，以控制向设计器和编辑器提供的上下文服务。|
|从 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>：<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|使项目子类型成为<br /><br /> -参与项目命令的命令路由。<br />-添加、删除或禁用项目环境命令，并解决方案资源管理器活动命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|启用项目子类型，以筛选用户在 "**添加新项**" 对话框中看到的内容。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|使项目子类型成为<br /><br /> -确定给定文件扩展名的默认生成器。<br />-将可读的生成器名称映射到 COM 对象。|

## <a name="properties-used-by-project-subtypes"></a>项目子类型使用的属性
 环境和基本项目系统可以使用下表中详细 <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> 和 <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> 枚举中的属性，使项目子类型能够控制项目系统的各种功能。

|VSHPROPID 属性|项目子类型|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|允许项目子类型控制 "**添加项**" 对话框的内容。 项目子类型可以提供新的模板目录规范、添加新类型的项、删除现有项以及重新组织基本项目的 "**添加项**" 对话框中的项的子集。|
|`PropertyPagesCLSIDList`|允许项目子类型添加或删除独立于配置的属性页。|
|`CfgPropertyPagesCLSIDList`|允许项目子类型添加或删除依赖于配置的属性页。|
|`ExtObjectCATID`|通过了解扩展程序 CATID，允许项目子类型为项目或项目项对象提供自动化扩展程序。 例如，项目子类型可以提供自定义的 `Project.Extender("<subtype>")` 对象。|
|`BrowseObjectCATID`|通过了解扩展程序 CATID，允许项目子类型为 `Browse` 对象提供自动化扩展程序。 例如，项目子类型可以将额外的属性添加到 <xref:EnvDTE.Project.Properties%2A> 集合。|
|`CfgBrowseObjectCATID`|允许项目子类型为项目配置浏览对象提供自动化扩展程序。 例如，项目子类型可以将额外的属性添加到 <xref:EnvDTE.Configuration.Properties%2A> 集合。|
|`CfgExtObjectCATID`|允许项目子类型为配置对象提供自动化扩展程序。|
|`DefaultPlatformName`|允许项目子类型确定项目的配置对象的平台名称。|

 基本项目提供上述属性的默认实现。 基项目通过对最外面的项目子类型的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 调用 `QueryInterface` 获取这些属性，从而允许项目子类型重写属性的实现。

## <a name="see-also"></a>请参阅
- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)