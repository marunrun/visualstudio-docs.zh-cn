---
title: 扩展基项目的对象模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7723881bce81824b66a936793175077a0ec67666
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187169"
---
# <a name="extending-the-object-model-of-the-base-project"></a>扩展基项目的对象模型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可以在以下位置扩展基本项目的自动化对象模型：  
  
-  ( " \<ProjectSubtypeName> " ) ，这允许项目子类型使用中的自定义方法来提供对象 <xref:EnvDTE.Project> 。 项目子类型可以使用自动化扩展器来公开 `Project` 对象。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口应为 `VSHPROPID_ExtObjectCATID` 从 <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>) CATID 中的值 VSITEMID_ROOT 的 (提供其对象 `itemid` `VSITEMID` 。  
  
- 项目项. 扩展程序 ( " \<ProjectSubtypeName> " ) -这允许项目子类型为对象提供来自项目内特定对象的自定义方法 <xref:EnvDTE.ProjectItem> 。 项目子类型可以使用自动化扩展器来公开此对象。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口需要为 `VSHPROPID_ExtObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> 对应于所需) CATID 的 from (提供其对象 `VSITEMID` 。  
  
- 项目属性–此集合公开对象的配置独立属性 `Project` 。 有关项目属性的详细信息，请参阅 <xref:EnvDTE.Project.Properties%2A> 。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口需要为 VSHPROPID2 提供其对象 `VSHPROPID_BrowseObjectCATID` ， (与 VSITEMID_ROOT 的 `itemid` 值相对应， <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>) CATID。  
  
- Properties –此集合为特定配置公开项目的配置依赖属性 (例如，调试) 。 有关详细信息，请参阅 <xref:EnvDTE.Configuration>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>在主项目子类型聚合器上实现的接口为 CATID (的对象提供 `VSHPROPID_CfgBrowseObjectCATID` 与 `itemid`) 的值对应的对象 <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>接口用于区分一个配置浏览对象和另一个。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
