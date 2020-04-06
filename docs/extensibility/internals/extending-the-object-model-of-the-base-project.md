---
title: 扩展基础项目的对象模型 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708401"
---
# <a name="extend-the-object-model-of-the-base-project"></a>扩展基础项目的对象模型

项目子类型可在以下位置扩展基础项目的自动化对象模型：

- Project.Extender（"\<项目子类型名称>"）：这允许项目子类型提供<xref:EnvDTE.Project>具有对象自定义方法的对象。 项目子类型可以使用自动化扩展器公开对象`Project`。 在<xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现的接口应提供`VSHPROPID_ExtObjectCATID`其对象为 from（<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>对应于`itemid` [VSITEMID 的值）。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)） CATID。

- ProjectItem.Extender（"\<项目子类型名称>"）：这允许项目子类型提供具有项目中特定<xref:EnvDTE.ProjectItem>对象的自定义方法的对象。 项目子类型可以使用自动化扩展器公开此对象。 在<xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现的接口需要为`VSHPROPID_ExtObjectCATID`来自<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>（对应于<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>） CATID 提供其对象。

- Project.属性：此集合公开`Project`对象与配置无关的属性。 有关 `Project` 属性的详细信息，请参阅 <xref:EnvDTE.Project.Properties%2A>。 项目子类型可以使用自动化扩展器将其属性添加到此集合。 在<xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现的接口需要为`VSHPROPID_BrowseObjectCATID`提供其<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>对象（对应于`itemid`[VSITEMID 的值）。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)） CATID。

- 配置.属性：此集合公开特定配置的项目的与配置相关的属性（例如，调试）。 有关详细信息，请参阅 <xref:EnvDTE.Configuration>。 项目子类型可以使用自动化扩展器将其属性添加到此集合。 在<xref:EnvDTE80.IInternalExtenderProvider>主项目子类型聚合器上实现的接口为 CATID`VSHPROPID_CfgBrowseObjectCATID`提供其对象（对应于`itemid`[VSITEMID 的值）。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)）。 该<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>接口用于区分一个配置浏览对象和另一个配置浏览对象。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
