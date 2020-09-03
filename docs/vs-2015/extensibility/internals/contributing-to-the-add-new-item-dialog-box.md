---
title: 参与 "添加新项" 对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d288f2d007fd0f923021847179326069959d3698
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197027"
---
# <a name="contributing-to-the-add-new-item-dialog-box"></a>构成“添加新项”对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可以通过注册 "添加新项" 对话框中的 "添加**项**模板"，为 "**添加新项**" 对话框提供一个完整的新目录 `Projects` 。  
  
## <a name="registering-add-new-item-templates"></a>注册 "添加新项" 模板  
 此部分位于注册表中 **HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0\projects** 下。 下面的注册表项假定 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 项目由假设项目子类型聚合。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]下面列出了项目的条目。  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]  
@="#2143"  
"DefaultProjectExtension"="vbproj"  
"PossibleProjectExtensions"="vbproj;vbp"  
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]  
@="#100"  
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"  
```  
  
 `AddItemTemplates\TemplateDirs`子项包含注册表项，其中包含指向 "**添加新项**" 对话框中可用项的目录的路径。  
  
 环境自动加载 `AddItemTemplates` 注册表子项下的所有数据 `Projects` 。 这可能包括用于基本项目实现的数据，以及特定项目子类型类型的数据。 每个项目子类型都由项目类型标识 `GUID` 。 项目子类型可以指定应将一组备用 `Add Item` 模板用于特定的风格项目实例，方法是支持中的 `VSHPROPID_ AddItemTemplatesGuid` 枚举 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 以返回项目子类型的 GUID 值。 如果 `VSHPROPID_AddItemTemplatesGuid` 未指定属性，则使用基本项目 GUID。  
  
 您可以通过在 " **添加新项** " 对话框中实现 " <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> 项目子类型" 聚合对象上的接口来筛选项。 例如，通过聚合项目实现数据库项目的项目子类型， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 可以 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 通过实现筛选来筛选 " **添加新项** " 对话框中的特定项，进而通过支持中的来添加特定于数据库项目的项 `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 。 有关筛选和添加项到 " **添加新项** " 对话框的详细信息，请参阅将 [项添加到 "添加新项" 对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
