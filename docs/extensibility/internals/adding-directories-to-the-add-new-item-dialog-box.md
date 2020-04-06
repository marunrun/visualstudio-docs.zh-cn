---
title: 将目录添加到"添加新项目"对话框 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d4af79f95c87271e9a10eece6c728daa9a81305
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710254"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>将目录添加到"添加新项目"对话框
以下代码示例演示如何为 **"添加新项目"** 对话框注册一组新的目录。 **"添加新项目"** 对话框的目录对于每个项目都不同。 因此，目录在 **"项目**子键"下注册，HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_8.0Exp_**项目**。

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

 该`%Template_Path%`值指定包含项目模板的目录的完整路径。 这些模板可以是 *.vsz*文件或要克隆的原型模板文件。

 该`SortPriority`值指定排序优先级。

## <a name="add-items-to-an-existing-project"></a>将项目添加到现有项目
 您还可以将项添加到现有项目。 例如，对于[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目，您可以将项目添加到*\<根>_程序文件\微软可视化工作室_VC_CSharpProject项目_本地项目项目文件夹*。 在这种情况下，`%GUID_Project%`是 C# 项目的 GUID （#FAE04EC0-301F-11D3-BF4B-00C04F79EFBC]）。

 还可以通过编程项目子类型来扩展现有项目。 使用项目子类型，无需编写新的项目类型即可扩展项目。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [将项目添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到"新项目"对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
