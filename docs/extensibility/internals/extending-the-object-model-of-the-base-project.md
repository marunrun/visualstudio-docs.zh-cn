---
title: 扩展的基础项目对象模型 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 607a63dc84db2811a4a2d158be07f158b849e1ad
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329049"
---
# <a name="extend-the-object-model-of-the-base-project"></a>扩展的基础项目对象模型

项目子类型可能会扩展在以下位置中的基础项目的自动化对象模型：

- Project.Extender("\<ProjectSubtypeName>"):这样，项目子类型与自定义方法从提供对象<xref:EnvDTE.Project>对象。 项目子类型可以使用自动化扩展程序来公开`Project`对象。 <xref:EnvDTE80.IInternalExtenderProvider>接口实现的主项目子类型聚合器上应提供有关其对象`VSHPROPID_ExtObjectCATID`从<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>(对应于`itemid`的值[VSITEMID。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- ProjectItem.Extender("\<ProjectSubtypeName>"):这样，要使用自定义方法提供一个对象，从特定项目子类型<xref:EnvDTE.ProjectItem>在项目中的对象。 项目子类型可以使用自动化扩展程序公开此对象。 <xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现接口，需要提供有关其对象`VSHPROPID_ExtObjectCATID`从<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>(对应于所需<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>) CATID。

- Project.Properties:此集合公开的独立于配置的属性`Project`对象。 有关 `Project` 属性的详细信息，请参阅 <xref:EnvDTE.Project.Properties%2A>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现接口，需要提供有关其对象`VSHPROPID_BrowseObjectCATID`从<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>(对应于`itemid`的值[VSITEMID。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID。

- Configuration.Properties:此集合公开为 （例如，调试） 特定的配置项目的依赖于配置的属性。 有关详细信息，请参阅 <xref:EnvDTE.Configuration>。 项目子类型可以使用自动化扩展程序将其属性添加到此集合。 <xref:EnvDTE80.IInternalExtenderProvider>接口实现的主项目子类型聚合器上提供其对象的 CATID `VSHPROPID_CfgBrowseObjectCATID` (对应于`itemid`的值[VSITEMID。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>))。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>接口用于将一个配置浏览对象与另一种区分开来。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>