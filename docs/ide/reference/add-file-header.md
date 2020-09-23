---
title: 添加文件头
ms.date: 07/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 44c3b64d9fb8944a578d054b7d98d4bf39bde3bc
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810371"
---
# <a name="add-file-header"></a>添加文件头

此代码生成适用于：

- C#

- Visual Basic

**功能：** 使用 [EditorConfig](../create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project) 向现有文件、项目和解决方案添加文件头。

**使用时机：** 你希望能够轻松地向文件、项目和解决方案添加文件头。

操作原因：出于版权目的，你的团队要求你添加文件头。 

## <a name="how-to"></a>操作说明

1. 向项目或解决方案添加 [EditorConfig](../create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)（如果还没有的话）。

2. 将以下规则添加到 EditorConfig 文件：file_header_template。

3. 将规则的值设置为等于要应用的头文本。 对于文件名，可以使用 `{fileName}` 作为占位符。

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