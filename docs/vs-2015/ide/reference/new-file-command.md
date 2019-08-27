---
title: “新建文件”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.newfile
helpviewer_keywords:
- File.NewFile command
- New File command
ms.assetid: 767868d6-a525-425b-a43b-2198f636ab6b
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bb86a15e73ac2410ad763acd3b361e4a82bc44f1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199077"
---
# <a name="new-file-command"></a>“新建文件”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建新文件并将其打开。 该文件显示在“杂项文件”文件夹下。  
  
## <a name="syntax"></a>语法  
  
```  
File.NewFile [filename] [/t:templatename] [/editor:editorname]  
```  
  
## <a name="arguments"></a>自变量  
 `filename`  
 可选。 文件的名称。 如果未提供名称，则使用默认名称。 如果没有列出模板名称，则创建文本文件。  
  
## <a name="switches"></a>开关  
 /t:`templatename`  
 可选。 指定要创建的文件类型。  
  
 /t:`templatename` 参数语法反映在“新建文件”对话框中找到的信息。 输入类别名称，后跟反斜杠 (`\`) 和模板名称，然后用引号将整个字符串引起。  
  
 例如，要创建新的 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 文本文件，对于 /t:`templatename` 参数，应输入以下内容。  
  
```  
/t:"Visual C++\C++ File (.cpp)"  
```  
  
 以上示例指示 C++ 文件模板位于“新建文件”对话框中的 Visual C++ 类别下  。  
  
 /e:`editorname`  
 可选。 将在其中打开文件的编辑器的名称。 如果指定该参数，但未提供编辑器名称，则会出现“打开方式”  对话框。  
  
 /e:`editorname` 参数语法使用“打开方式”对话框中显示的编辑器名称，并用引号括起来。  
  
 例如，若要在源代码编辑器中打开文件，对于 /e:`editorname` 参数，应输入以下内容。  
  
```  
/e:"Source Code (text) Editor"  
```  
  
## <a name="example"></a>示例  
 此示例创建了新网页“test1.htm”，并在源代码编辑器中将其打开。  
  
```  
>File.NewFile test1 /t:"General\HTML Page" /e:"Source Code (text) Editor"  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [即时窗口](../../ide/reference/immediate-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
