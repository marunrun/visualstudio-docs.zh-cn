---
title: 将目录添加到 "添加新项" 对话框 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80710254"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>将目录添加到 "添加新项" 对话框
下面的代码示例演示如何为 " **添加新项** " 对话框注册一组新的目录。 每个项目的 " **添加新项** " 对话框的目录不同。 因此，在 " **项目** " 子项下注册目录， **HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp\projects**"中找到。

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

 `%Template_Path%`值指定包含项目模板的目录的完整路径。 这些模板可以是要克隆的 *.vsz* 文件或原型模板文件。

 `SortPriority`该值指定排序优先级。

## <a name="add-items-to-an-existing-project"></a>向现有项目中添加项
 你还可以向现有项目中添加项。 例如，对于 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目，可以向* \<root> \Program Files\Microsoft Visual Studio\VC # \CSharpProjectItems\LocalProjectItems*文件夹添加项。 在这种情况下， `%GUID_Project%` 是 c # 项目 ( {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC} ) 的 GUID。

 还可以通过编程项目子类型来扩展现有项目。 使用项目子类型，可以扩展项目，而无需编写新的项目类型。 有关项目子类型的详细信息，请参阅 [项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>另请参阅
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [将目录添加到 "新建项目" 对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
