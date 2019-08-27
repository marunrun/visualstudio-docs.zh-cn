---
title: 项目子类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5ad1e105d43c40782b13d8799b20626e57363c2f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63421834"
---
# <a name="project-subtypes"></a>项目子类型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目子类型可以自定义或 flavor 的项目系统的行为[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 自定义项包括其他数据保存在项目文件中，添加或筛选中的项**添加新项**对话框中，控制如何调试和部署，程序集和扩展项目**属性页**对话框。 Vspackage 实现项目子类型使用 COM 聚合。  
  
> [!NOTE]
> 视觉对象C++项目系统不支持项目子类型。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 使用项目子类型实现 SQL Server 和智能设备项目本身。  
  
## <a name="in-this-section"></a>本节内容  
 [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)  
 介绍项目子类型的概念。  
  
 [项目子类型的初始化序列](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)  
 介绍通过编程项目子类型初始化序列[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]环境。  
  
 [项目子类型扩展的属性和方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)  
 提供的功能和最常通过使用项目子类型扩展方法的详细的说明。  
  
 [保留 MSBuild 项目文件中的数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)  
 介绍如何将数据保存在项目文件以及如何使用<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>跨项目子类型聚合级别维护项目文件中的数据。  
  
 [项目属性用户界面](../../extensibility/internals/project-property-user-interface.md)  
 描述项目子类型可以如何修改项目**属性页**对话框。  
  
 [扩展基项目的对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)  
 提供有关项目子类型如何使用自动化扩展程序来扩展自动化对象模型的信息。  
  
 [构成“添加新项”对话框](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)  
 介绍如何将项添加到**添加新项**对话框。  
  
 [将数据保存在项目文件中](../../extensibility/saving-data-in-project-files.md)  
 介绍如何将保存并使用托管包框架 (MPF) 检索项目文件中的特定于子类型的数据项目子类型。  
  
 [处理专用部署](../../extensibility/internals/handling-specialized-deployment.md)  
 介绍了如何项目子类型可以提供专门的部署行为，通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>接口。  
  
 [添加和删除属性页](../../extensibility/adding-and-removing-property-pages.md)  
 介绍如何添加和删除项目设计器中的属性页。  
  
## <a name="related-sections"></a>相关章节  
 [项目类型](../../extensibility/internals/project-types.md)  
 提供了详细说明的主题的链接[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]项目。
