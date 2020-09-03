---
title: 扩展基项目的对象模型 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33186cd477ade7f562f6191393dabe8e94f4f194
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708401"
---
# <a name="extend-the-object-model-of-the-base-project"></a>扩展基项目的对象模型

项目子类型可以在以下位置扩展基本项目的自动化对象模型：

- 项目 ( " \<ProjectSubtypeName> " ) ：这允许项目子类型从对象提供具有自定义方法的对象 <xref:EnvDTE.Project> 。 项目子类型可以使用自动化扩展器来公开 `Project` 对象。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口应为与 `VSHPROPID_ExtObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> VSITEMID 值对应的 from (提供其对象 `itemid` [。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- 项目项 ( " \<ProjectSubtypeName> " ) ：这允许项目子类型从项目内的特定对象提供自定义方法的对象 <xref:EnvDTE.ProjectItem> 。 项目子类型可以使用自动化扩展器来公开此对象。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口需要为 `VSHPROPID_ExtObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> 对应于所需) CATID 的 from (提供其对象 <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> 。

- 项目. 属性：此集合公开对象的独立于配置的属性 `Project` 。 有关 `Project` 属性的详细信息，请参阅 <xref:EnvDTE.Project.Properties%2A>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口需要为 `VSHPROPID_BrowseObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> 对应于 VSITEMID 值的 from (提供其对象 `itemid` [。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- 配置属性：对于特定的配置，此集合显示项目的依赖于配置的属性 (例如，调试) 。 有关详细信息，请参阅 <xref:EnvDTE.Configuration>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口为 `VSHPROPID_CfgBrowseObjectCATID` 与 VSITEMID 值对应的 CATID (提供其对象 `itemid` [。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>接口用于区分一个配置浏览对象和另一个。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
