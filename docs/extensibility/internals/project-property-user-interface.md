---
title: 项目属性用户界面 |微软文档
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4634eb5edaab16752bc5df82d70371a580845d28
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706398"
---
# <a name="project-property-user-interface"></a>项目属性用户界面

项目子类型可以使用项目**属性页**对话框中的项，因为它们由基础项目提供，隐藏或使只读控件和整个页面提供，或将项目子类型特定的**页面添加到"属性页"** 对话框中。

## <a name="extending-the-project-property-dialog-box"></a>扩展项目属性对话框

项目子类型实现自动化扩展器和项目配置浏览对象。 这些扩展器实现<xref:EnvDTE.IFilterProperties>接口，使特定属性隐藏或只读。 基础项目的属性**页**对话框由基础项目实现，该对话框表示自动化扩展器执行的筛选。

扩展**项目属性**对话框的过程概述如下：

- 基本项目通过实现<xref:EnvDTE80.IInternalExtenderProvider>接口从项目子类型检索扩展器。 基础项目的浏览、项目自动化和项目配置浏览对象都实现了此接口。

- 项目浏览对象的<xref:EnvDTE80.IInternalExtenderProvider>实现<xref:EnvDTE80.IInternalExtenderProvider>和项目自动化对象委托给项目子类型聚合器的实现（即，它们`QueryInterface`用于<xref:EnvDTE80.IInternalExtenderProvider><xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>项目对象）。

- 基本项目配置浏览对象还实现<xref:EnvDTE80.IInternalExtenderProvider>直接从项目子类型配置对象连接到自动化扩展器中。 其实现委托给项目子<xref:EnvDTE80.IInternalExtenderProvider>类型聚合器实现的接口。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>，由项目配置浏览对象实现，返回对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>，也实现由项目配置浏览对象，返回<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>对象。

- 项目子类型可以通过检索以下<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>值来确定基本项目在运行时的各种可扩展对象的相应 CATID：

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_ExtObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_BrowseObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_CfgBrowseObjectCATID>

要确定项目作用域的 CATID，项目子类型将检索 VSITEMID 的上述属性[。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)从`VSITEMID typedef`。 项目子类型可能还希望控制为项目显示哪些**属性页**对话框页，这两个页面都与配置无关，并且与配置无关。 某些项目子类型可能需要删除内置页面并添加项目子类型特定页面。 为了启用此功能，托管客户端项目调用以下属性<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>的方法：

- `VSHPROPID_PropertyPagesCLSIDList`• 与配置无关的属性页的 CLSID 的分号分隔列表。

- `VSHPROPID_CfgPropertyPagesCLSIDList —`与配置相关的属性页的 CLSID 的分号分隔列表。

由于项目子类型聚合<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象，它可以覆盖这些属性的定义，以控制显示的属性**页**对话框。 项目子类型可以从内部基项目中检索这些属性，然后根据需要添加或删除 CLSID。

项目子类型添加的新属性页将从基础项目实现中传递项目配置浏览对象。 此项目配置浏览对象支持自动化扩展器。 有关自动化扩展器的详细信息，请参阅[实现和使用自动化扩展器](https://msdn.microsoft.com/Library/0d5c218c-f412-4b28-ab0c-33a611f62356)。 项目子类型调用<xref:EnvDTE.Project.Extender%2A>实现的属性页，用于检索其自己的项目子类型配置浏览对象，该对象扩展了基础项目的配置浏览对象。

## <a name="see-also"></a>请参阅

- <xref:EnvDTE.IFilterProperties>
- [属性页对话框](/previous-versions/visualstudio/visual-studio-2010/as5chysf(v=vs.100))
