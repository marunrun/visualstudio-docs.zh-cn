---
title: “新建文件”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.newfile
helpviewer_keywords:
- File.NewFile command
- New File command
ms.assetid: 767868d6-a525-425b-a43b-2198f636ab6b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5fe8a99ee59a347fdcb7cff601b75139760630f7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595951"
---
# <a name="new-file-command"></a>“新建文件”命令
创建新文件并将其打开。 该文件显示在“杂项文件”文件夹下。

## <a name="syntax"></a>语法

```cmd
File.NewFile [filename] [/t:templatename] [/editor:editorname]
```

## <a name="arguments"></a>自变量
`filename`

可选。 文件的名称。 如果未提供名称，则使用默认名称。 如果没有列出模板名称，则创建文本文件。

## <a name="switches"></a>开关
/t:`templatename`\
可选。 指定要创建的文件类型。

/t:`templatename` 参数语法反映在“新建文件”对话框中找到的信息。 输入类别名称，后跟反斜杠 (`\`) 和模板名称，然后用引号将整个字符串引起。

例如，要创建新的 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 文本文件，对于 /t:`templatename` 参数，应输入以下内容。

```cmd
/t:"Visual C++\C++ File (.cpp)"
```

以上示例指示 C++ 文件模板位于“新建文件”对话框中的 Visual C++ 类别下  。

/e:`editorname`\
可选。 将在其中打开文件的编辑器的名称。 如果指定该参数，但未提供编辑器名称，则会出现“打开方式”  对话框。

/e:`editorname` 参数语法使用“打开方式”对话框中显示的编辑器名称，并用引号括起来。

例如，若要在源代码编辑器中打开文件，对于 /e:`editorname` 参数，应输入以下内容。

```cmd
/e:"Source Code (text) Editor"
```

## <a name="example"></a>示例
此示例创建了新网页“test1.htm”，并在源代码编辑器中将其打开。

```cmd
>File.NewFile test1 /t:"General\HTML Page" /e:"Source Code (text) Editor"
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [即时窗口](../../ide/reference/immediate-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
