---
title: 项目属性用户界面 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a83e5c9fb633322da536e62f1ba03484b965b162
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71252343"
---
# <a name="project-property-user-interface"></a>项目属性用户界面

项目子类型可以使用 "项目**属性页**" 对话框中的项，因为它们由基本项目提供、隐藏或使只读控件和整页提供，或将特定于项目子类型的页添加到 "**属性页**" 对话框文本框.

## <a name="extending-the-project-property-dialog-box"></a>扩展 "项目属性" 对话框

项目子类型实现自动化扩展程序和项目配置浏览对象。 这些扩展程序实现<xref:EnvDTE.IFilterProperties>了接口，以使特定属性处于隐藏或只读状态。 基本项目实现的基本项目的 "**属性页**" 对话框将遵循自动化扩展程序执行的筛选。

下面概述了扩展**项目属性**对话框的过程：

- 基项目通过实现<xref:EnvDTE80.IInternalExtenderProvider>接口，从项目子类型中检索扩展程序。 基本项目的 "浏览"、"项目自动化" 和 "项目配置" 浏览对象均实现此接口。

- `QueryInterface` <xref:EnvDTE80.IInternalExtenderProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:EnvDTE80.IInternalExtenderProvider>项目的 "浏览对象" 和 "项目自动化对象委托" 委托给项目子类型聚合器的实现（即，它们适用于<xref:EnvDTE80.IInternalExtenderProvider>项目对象）。

- 基本项目配置 "浏览" 对象还<xref:EnvDTE80.IInternalExtenderProvider>实现了从 "项目子类型" 配置对象直接连接到自动化扩展器。 其实现委托给<xref:EnvDTE80.IInternalExtenderProvider>由项目子类型聚合器实现的接口。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>由 "项目配置" 浏览对象实现，返回<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>还由项目配置浏览对象实现，它返回<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>对象。

- 项目子类型可以通过检索以下<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>值在运行时为基本项目的各种可扩展对象确定相应的 catid：

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_ExtObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_BrowseObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_CfgBrowseObjectCATID>

若要确定项目范围的 Catid，项目子类型将检索 VSITEMID 的上述属性[。](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)中的`VSITEMID typedef`根。 项目子类型还可能需要控制为项目显示的 "**属性页**" 对话框页，分别为配置依赖项和独立配置。 某些项目子类型可能需要删除内置页面并添加特定于项目子类型的页面。 为实现此目的，托管客户端项目对以下属性<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>调用方法：

- `VSHPROPID_PropertyPagesCLSIDList`-以分号分隔的、独立于配置的属性页的 Clsid 列表。

- `VSHPROPID_CfgPropertyPagesCLSIDList —`依赖于配置的属性页的 Clsid 列表（以分号分隔）。

由于项目子类型聚合<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象，因此它可以重写这些属性的定义以控制显示哪些**属性页**对话框。 项目子类型可以从内部基础项目中检索这些属性，并根据需要添加或删除 Clsid。

项目子类型添加的新属性页将从基本项目实现中传递项目配置浏览对象。 此项目配置浏览对象支持自动化扩展程序。 有关 AutomationExtenders 的详细信息，请参阅[实现和使用自动化扩展](https://msdn.microsoft.com/Library/0d5c218c-f412-4b28-ab0c-33a611f62356)程序。 由项目子类型调用<xref:EnvDTE.Project.Extender%2A>实现的属性页检索其自己的项目子类型配置浏览对象，该对象扩展了基项目的配置浏览对象。

## <a name="see-also"></a>请参阅

- <xref:EnvDTE.IFilterProperties>
- ["属性页" 对话框](/previous-versions/visualstudio/visual-studio-2010/as5chysf(v=vs.100))
