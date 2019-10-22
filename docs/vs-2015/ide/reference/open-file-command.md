---
title: “打开文件”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.openfile
helpviewer_keywords:
- Open File command
- File.OpenFile command
- of command
ms.assetid: a51a83fc-e3c6-4fa2-8882-8b7b6c0a6406
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1c8dcf35e4c045db0d9acd45e2eb307a31ba39f1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671937"
---
# <a name="open-file-command"></a>“打开文件”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

打开现有文件，并允许指定编辑器。

## <a name="syntax"></a>语法

```
File.OpenFile filename [/e:editorname]
```

## <a name="arguments"></a>自变量
 `filename`（必需）。 要打开的文件的完整或部分路径和文件名。 包含空格的路径必须引在引号内。

## <a name="switches"></a>开关
 /e:`editorname`（可选）。 将在其中打开文件的编辑器的名称。 如果指定该参数，但未提供编辑器名称，则会出现“打开方式”  对话框。

 /e:`editorname` 参数语法使用“打开方式”对话框中显示的编辑器名称，并用引号括起来。

 例如，若要在源代码编辑器中打开文件，对于 /e:`editorname` 参数，应输入以下内容。

```
/e:"Source Code (text) Editor"
```

## <a name="remarks"></a>备注
 输入路径时，自动补全功能会尝试查找正确的路径和文件名。

## <a name="example"></a>示例
 此示例在源代码编辑器中打开样式文件“Test1.css”。

```
>File.OpenFile "C:\My Projects\project1\Test1.css" /e:"Source Code (text) Editor"
```

## <a name="see-also"></a>另请参阅
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)[窗口](../../ide/reference/command-window.md)[即时窗口](../../ide/reference/immediate-window.md) ["查找/命令" 框](../../ide/find-command-box.md) [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
