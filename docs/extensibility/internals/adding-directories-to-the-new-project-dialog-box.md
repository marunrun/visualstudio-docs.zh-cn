---
title: 将目录添加到新建项目对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e81d09c2a4e97ca5f3da112e593b04b219e6314
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328003"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>将目录添加到新建项目对话框
在创建新的项目类型时，你还可以注册中的新目录**新的项目**对话框来显示它们用于作为模板。 下面的代码示例说明如何注册一个新目录，也称为节点。 在示例中，模板由 VSPackage *CLSID_Package*，注册。 因此，左侧和右侧的**新的项目**对话框提供了添加的节点，名称由*Folder_Label_ResID*资源。 从 VSPackage 附属 DLL 中加载此资源。

 **文件夹**值表示在其下的文件夹的 GUID *Folder_Label_ResID*节点都将显示。 在示例中，GUID 表示**其他项目**中的文件夹**项目类型**窗格**新项目**对话框。 如果**其他项目**值不存在，标签将置于最高级别。

 `TemplatesDir`值指定包含的项目模板的目录的完整路径。 这些文件可以是 *.vsz*文件或要克隆的典型的模板文件。

 如果指定`TemplatesLocalizedSubDir`，它必须是命名的子目录的字符串的资源 ID`TemplatesDir`保存已本地化的模板。 因为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载字符串资源从附属 DLL 如果有帐户，每个附属 DLL 可以包含不同子目录的名称。 `SortPriority`值指定排序优先级。

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
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [将项目添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到添加新项对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)