---
title: 将目录添加到新项目对话框 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 827e383bba13c9742deb654bf3d680adeb3c109b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710243"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>将目录添加到"新项目"对话框
创建新项目类型时，还可以在 **"新项目"** 对话框中注册新目录以将其显示为模板。 以下代码示例说明了如何注册新目录（也称为节点）。 在此示例中，VSPackage 公开的模板*CLSID_Package*， 注册。 因此，"**新项目"** 对话框的左侧提供添加的节点，名称由*Folder_Label_ResID*资源确定。 此资源从 VSPackage 卫星 DLL 加载。

 **"文件夹**"值表示显示*Folder_Label_ResID*节点的文件夹的 GUID。 在此示例中，GUID 表示 **"新项目**"对话框"**项目类型"** 窗格中的 **"其他项目**"文件夹。 如果 **"其他项目**"值不存在，则标签将放置在顶层。

 该`TemplatesDir`值指定包含项目模板的目录的完整路径。 这些文件可以是 *.vsz*文件或要克隆的典型模板文件。

 如果指定`TemplatesLocalizedSubDir`，它必须是命名保存本地化模板的子目录的`TemplatesDir`字符串的资源 ID。 由于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]如果具有一个子目录，则从附属 DLL 加载字符串资源，因此每个附属 DLL 可以包含不同的子目录名称。 该`SortPriority`值指定排序优先级。

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
- [注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [将项目添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到"添加新项目"对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
