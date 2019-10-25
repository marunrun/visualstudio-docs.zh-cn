---
title: “添加新项”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- project.addnewitem
helpviewer_keywords:
- Add New Item command
- File.AddNewItem command
ms.assetid: 63b7df32-db83-463b-bbe7-7ff011fe5298
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 683a65ab0c25a5daeb002a4eb3106006655a1b00
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748826"
---
# <a name="add-new-item-command"></a>“添加新项”命令
将新的解决方案项，如.htm、.css、.txt 或框架集添加到当前解决方案中并打开它。

## <a name="syntax"></a>语法

```cmd
File.AddNewItem [filename] [/t:templatename] [/e:editorname]
```

## <a name="arguments"></a>自变量
`filename`\
可选。 要添加到解决方案的项的路径和文件名。

## <a name="switches"></a>开关
/t: `templatename`\
可选。 指定要创建的文件类型。 如果未给定模板名称，则默认创建一个文本文件。

/t:`templatename` 参数语法反映在“添加新解决方案项”  对话框中找到的信息。 必须输入完整类别，后跟文件类型，类别名称与文件类型用反斜杠 (`\`) 隔开，并将整个字符串括在引号内。

例如，若要创建新的文本文件，对于 /t:`templatename` 参数，应输入以下内容。

```cmd
/t:"General\Style Sheet"
```

/e: `editorname`\
可选。 将在其中打开文件的编辑器的名称。 如果指定该参数，但未提供编辑器名称，则会出现“打开方式”  对话框。

/e:`editorname` 参数语法使用“打开方式”  对话框中显示的编辑器名称，并用引号括起来。

例如，若要在源代码编辑器中打开样式表，对于 /e:`editorname` 参数，应输入以下内容。

```cmd
/e:"Source Code (text) Editor"
```

## <a name="example"></a>示例
此示例向当前解决方案添加新的解决方案项 MyHTMLpg。

```cmd
>File.AddNewItem MyHTMLpg /t:"General\HTML Page"
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)