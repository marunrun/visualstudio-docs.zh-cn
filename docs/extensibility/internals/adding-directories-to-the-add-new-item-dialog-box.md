---
title: 将目录添加到添加新建项对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 981b65df9354277580ee1c816f4e0fd0977f9a85
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328021"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>将目录添加到添加新项对话框
下面的代码示例演示如何注册一组新的目录**添加新项**对话框。 目录**添加新项**对话框是不同的每个项目。 因此下, 注册目录**项目**子项中, 找到**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects**。

## <a name="registry-script"></a>注册表脚本

```
NoRemove Projects
{
  NoRemove %GUID_Project%
  {
    NoRemove AddItemTemplates
    {
      NoRemove TemplateDirs
      {
        ForceRemove %CLSID_Package%
        {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
          {
            val TemplatesDir = s '%Template_Path%'
            val SortPriority = d 2000
          }
        }
      }
    }
  }
}
```

 `%Template_Path%`值指定包含的项目模板的目录的完整路径。 这些模板可以是 *.vsz*文件或要克隆的原型的模板文件。

 `SortPriority`值指定排序优先级。

## <a name="add-items-to-an-existing-project"></a>将项添加到现有项目
 此外可以向现有项目添加项。 例如，对于[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目中，您可以将项添加到 *\<根 > \Program Files\Microsoft Visual Studio\VC #\CSharpProjectItems\LocalProjectItems* 文件夹。 在这种情况下，`%GUID_Project%`是 C# 项目 ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}) 的 GUID。

 此外可以通过编程项目子类型来扩展现有的项目。 项目子类型，而无需编写新的项目类型可以扩展项目。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [将项目添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到新建项目对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)