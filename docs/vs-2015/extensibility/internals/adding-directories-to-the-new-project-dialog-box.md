---
title: 将目录添加到 "新建项目" 对话框 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203874"
---
# <a name="adding-directories-to-the-new-project-dialog-box"></a>将目录添加到“新建项目”对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建新的项目类型时，还可以在 " **新建项目** " 对话框中注册一个新的目录，以将其显示为模板。 下面的代码示例说明了如何注册新目录（也称为节点）。 在此示例中，注册了 VSPackage CLSID_Package 公开的模板。 因此，" **新建项目** " 对话框的左侧提供添加的节点，名称由 Folder_Label_ResID 资源确定。 此资源从 VSPackage 附属 DLL 加载。  
  
 **文件夹**值表示在其下显示 Folder_Label_ResID 节点的文件夹的 GUID。 在此示例中，GUID 表示 "**新建项目**" 对话框的 "**项目类型**" 窗格中的 "**其他项目**" 文件夹。 如果缺少 **其他项目** 值，标签将定位在顶层。  
  
 TemplatesDir 值指定包含项目模板的目录的完整路径。 这些文件可以是要克隆的 .vsz 文件或典型模板文件。  
  
 如果指定 TemplatesLocalizedSubDir，则它必须是一个字符串的资源 ID，该字符串命名包含本地化模板的 TemplatesDir 的子目录。 由于 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 从附属 dll 加载字符串资源（如果有），因此每个附属 dll 都可以包含不同的子目录名称。 SortPriority 值指定排序优先级。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [将目录添加到“添加新项”对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
