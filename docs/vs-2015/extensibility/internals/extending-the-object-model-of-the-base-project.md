---
title: 扩展的基础项目对象模型 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187169"
---
# <a name="extending-the-object-model-of-the-base-project"></a>扩展基项目的对象模型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可能会扩展在以下位置中的基础项目的自动化对象模型：  
  
- Project.Extender ("\<ProjectSubtypeName >") – 这样，项目子类型与自定义方法从提供对象<xref:EnvDTE.Project>。 项目子类型可以使用自动化扩展程序来公开`Project`对象。 <xref:EnvDTE80.IInternalExtenderProvider>接口实现的主项目子类型聚合器上应提供有关其对象`VSHPROPID_ExtObjectCATID`从<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>(对应于`itemid`VSITEMID_ROOT，值从`VSITEMID`) CATID。  
  
- ProjectItem.Extender ("\<ProjectSubtypeName >") – 这样，要使用自定义方法提供一个对象，从特定项目子类型<xref:EnvDTE.ProjectItem>在项目中的对象。 项目子类型可以使用自动化扩展程序公开此对象。 <xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现接口，需要提供有关其对象`VSHPROPID_ExtObjectCATID`从<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>(对应于所需`VSITEMID`) CATID。  
  
- Project.Properties – 此集合公开的配置独立属性`Project`对象。 项目属性的详细信息，请参阅<xref:EnvDTE.Project.Properties%2A>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现接口，需要提供有关其对象`VSHPROPID_BrowseObjectCATID`从 VSHPROPID2 (对应于`itemid`VSITEMID_ROOT，值从<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>) CATID。  
  
- Configuration.Properties – 此集合公开为 （例如，调试） 特定的配置项目的配置依赖属性。 有关详细信息，请参阅 <xref:EnvDTE.Configuration>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>接口实现的主项目子类型聚合器上提供其对象的 CATID `VSHPROPID_CfgBrowseObjectCATID` (对应于`itemid`的值<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>)。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>接口用于将一个配置浏览对象与另一种区分开来。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
