---
title: 将目录添加到新建项目对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a8a9eeca4dc455c4f16e3551541454483138a993
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203874"
---
# <a name="adding-directories-to-the-new-project-dialog-box"></a>将目录添加到“新建项目”对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在创建新的项目类型时，你还可以注册中的新目录**新的项目**对话框来显示它们用于作为模板。 下面的代码示例说明如何注册一个新目录，也称为节点。 在示例中，会注册 VSPackage CLSID_Package 公开的模板。 因此，左侧和右侧的**新的项目**对话框提供了添加的节点，由 Folder_Label_ResID 资源的名称。 从 VSPackage 附属 DLL 中加载此资源。  
  
 **文件夹**值表示 Folder_Label_ResID 节点显示在其下的文件夹的 GUID。 在示例中，GUID 表示**其他项目**中的文件夹**项目类型**窗格**新项目**对话框。 如果**其他项目**值不存在，标签将置于最高级别。  
  
 TemplatesDir 值指定包含的项目模板的目录的完整路径。 这些文件可以是.vsz 文件或要克隆的典型的模板文件。  
  
 如果指定 TemplatesLocalizedSubDir，它必须是字符串的命名的子目录 TemplatesDir 包含本地化的模板的资源 ID。 因为[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]加载字符串资源从附属 DLL 如果有帐户，每个附属 DLL 可以包含不同子目录的名称。 SortPriority 值指定排序优先级。  
  
```  
NoRemove NewProjectTemplates  
{  
    NoRemove TemplateDirs  
  {  
    ForceRemove %CLSID_Package%  
    {  
      ForceRemove /1 = s '#%Folder_Label_ResID%'  
      {  
        val Folder = s '{DCF2A94A-45B0-11D1-ADBF-00C04FB6BE4C}'  
        val TemplatesDir = s '%Template_Path%'  
        val TemplatesLocalizedSubDir = s '#100'  
        val SortPriority = d 1000  
      }  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [将项添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [将目录添加到“添加新项”对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
