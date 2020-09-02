---
title: “添加现有项”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- project.addexistingitem
helpviewer_keywords:
- File.AddExistingItem command
- Add Existing Item command
ms.assetid: 41f56131-d4c7-4f81-83b7-bdac713ea870
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c2f636c2a0eb2cfdcebf383fdc7eea70f72cb90e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670224"
---
# <a name="add-existing-item-command"></a>“添加现有项”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将现有文件添加到当前解决方案中并打开它。

## <a name="syntax"></a>语法

```
File.AddExistingItem filename [/e:editorname]
```

## <a name="arguments"></a>参数
 `filename`（必需）。 待添加到当前解决方案的项的完整路径、文件名称和扩展名。 如果文件路径或文件名称包含空格，则将整个路径放在引号内。

## <a name="switches"></a>开关
 /e: `editorname`（可选）。 将在其中打开文件的编辑器的名称。 如果指定该参数，但未提供编辑器名称，则会出现“打开方式”**** 对话框。

 /e:`editorname` 参数语法使用“打开方式”**** 对话框中显示的编辑器名称，并用引号括起来。 例如，若要在源代码编辑器中打开样式表，对于 /e:`editorname` 参数，应输入以下内容。

```
/e:"Source Code (text) Editor"
```

## <a name="remarks"></a>备注
 键入内容时，自动完成功能会尝试查找正确的路径和文件名。

## <a name="example"></a>示例
 此示例向当前解决方案中添加文件 Form1.frm。

```
>File.AddExistingItem "C:\public\solution files\Form1.frm"
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) " [命令" 窗口](../../ide/reference/command-window.md)中的 ["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
