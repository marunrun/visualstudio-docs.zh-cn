---
title: 添加文件头
ms.date: 07/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 779092e277ac5b6eed3afcaceaf55b26ee2759dd
ms.sourcegitcommit: 025816f8e388b29e58761d304b0fda755ac5a613
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2020
ms.locfileid: "86374164"
---
# <a name="add-file-header"></a>添加文件头

此代码生成适用于：

- C#

- Visual Basic

**功能：** 使用 [EditorConfig](https://docs.microsoft.com/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project) 向现有文件、项目和解决方案添加文件头。

**使用时机：** 你希望能够轻松地向文件、项目和解决方案添加文件头。

操作原因：出于版权目的，你的团队要求你添加文件头。 

## <a name="how-to"></a>操作说明

1. 向项目或解决方案添加 [EditorConfig](https://docs.microsoft.com/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project)（如果还没有的话）。

2. 将以下规则添加到 EditorConfig 文件：file_header_template。

3. 将规则的值设置为等于要应用的头文本。

    ![EditorConfig 文件头规则](media/add-file-header-rule.png)

> [!NOTE]
> EditorConfig 中不能有显式多行，你需要使用 Unix 换行符来插入新行。

4. 将插入点置于任何 C# 或 Visual Basic 文件的第一行。

5. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

6. 选择“添加文件头”。 

    ![EditorConfig 文件头规则](media/add-file-header.png)

7. 若要将文件头应用于整个项目或解决方案，请选择“修复以下对象中的所有实例:”选项下面的“项目”或“解决方案”。

8. 此时，“修复所有实例”对话框打开，你可以在其中预览更改。

    ![“修复所有实例”对话框](media/file-header-preview-changes.png)

8. 选择“应用”，以应用更改。

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
