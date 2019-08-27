---
title: 项目属性用户界面 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31840c40f2a494ffd32f5241e2770938138877e9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704090"
---
# <a name="project-property-user-interface"></a>项目属性用户界面
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可以在项目中使用的项**属性页**对话框中为它们提供的基础项目中，隐藏或使只读控件和的整个页面提供，或将项目子类型特定于页面添加到**属性页**对话框。  
  
## <a name="extending-the-project-property-dialog-box"></a>扩展项目属性对话框  
 项目子类型实现自动化扩展程序和项目配置浏览对象。 这些扩展程序实现<xref:EnvDTE.IFilterProperties>接口以使特定的属性隐藏或只读的。 **属性页**对话框中的基础项目，实现基本的项目，遵循由自动化扩展程序执行的筛选。  
  
 扩展的进程**项目属性**下面列出了在对话框中：  
  
- 基础项目可检索项目子类型通过实现扩展程序<xref:EnvDTE80.IInternalExtenderProvider>接口。 浏览、 项目自动化和所有的基础项目的项目配置浏览对象实现此接口。  
  
- 实现<xref:EnvDTE80.IInternalExtenderProvider>为项目浏览对象和项目自动化对象委托给<xref:EnvDTE80.IInternalExtenderProvider>项目子类型聚合器的实现 (也就是说，它们`QueryInterface`有关<xref:EnvDTE80.IInternalExtenderProvider>上<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>项目对象）。  
  
- 基础项目配置浏览对象还实现<xref:EnvDTE80.IInternalExtenderProvider>以直接在项目子类型配置对象从自动化扩展程序关联。 其实现委托给<xref:EnvDTE80.IInternalExtenderProvider>由项目子类型聚合器实现的接口。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>由项目配置浏览对象，返回实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>由项目配置浏览对象，返回还实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>对象。  
  
- 项目子类型可以通过检索以下来确定在运行时的基础项目的各种可扩展对象相应 Catid<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>值：  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  若要确定项目范围的 Catid，项目子类型检索的上述属性<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>从`VSITEMID``typedef`。 项目子类型可能还想要控制哪些**属性页**对话框页面显示项目中，依赖于配置和独立的配置。 某些项目子类型可能需要删除内置页，并添加项目子类型特定页。 若要启用此选项，托管客户端项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>方法的以下属性：  
  
- `VSHPROPID_PropertyPagesCLSIDList` -独立于配置的属性页的 Clsid 的以分号分隔列表。  
  
- `VSHPROPID_CfgPropertyPagesCLSIDList —` 以分号分隔的 Clsid 依赖于配置的属性页的列表。  
  
  因为项目子类型的聚合<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>对象，它会重写的定义这些属性，以控制哪些**属性页**显示的对话框。 项目子类型可以检索这些属性的内部基础项目，然后添加或删除根据需要的 Clsid。  
  
  新添加的项目子类型的属性页都从基础项目实现传递的项目配置浏览对象。 此项目配置浏览对象支持自动化扩展程序。 AutomationExtenders 的详细信息，请参阅[实现并使用自动化扩展程序](https://msdn.microsoft.com/library/0d5c218c-f412-4b28-ab0c-33a611f62356)。 项目子类型调用由实现的属性页<xref:EnvDTE.Project.Extender%2A>来检索扩展基项目的配置浏览对象自己项目子类型配置浏览对象。  
  
## <a name="see-also"></a>请参阅  
 <xref:EnvDTE.IFilterProperties>   
 [属性页对话框](https://msdn.microsoft.com/4a3d34ac-ed03-45e8-ae60-a0e1aad300e4)
