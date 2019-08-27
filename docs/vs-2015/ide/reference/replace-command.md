---
title: Replace 命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.replace
helpviewer_keywords:
- Edit.Replace command
- Replace command
ms.assetid: a15767f1-5a3d-44f5-8c77-7b0f1157f340
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4ef58a39f1ff96a3c72cbb5a48940e378997cbca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157814"
---
# <a name="replace-command"></a>Replace 命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“查找和替换”窗口的“在文件中替换”选项卡上的可用选项子集替换文件中的文本   。  
  
## <a name="syntax"></a>语法  
  
```  
Edit.Replace findwhat replacewith [/all] [/case]  
[/doc|/proc|/open|/sel] [/hidden] [/options] [/reset] [/up]  
[/wild|/regex] [/word]  
```  
  
## <a name="arguments"></a>自变量  
 `findwhat`  
 必需。 要匹配的文本。  
  
 `replacewith`  
 必需。 用于替换匹配文本的文本。  
  
## <a name="switches"></a>开关  
 /all 或 /a  
 可选。 使用替换文本替换搜索文本的所有匹配项。  
  
 /case 或 /c  
 可选。 仅当大小写字符和 `findwhat` 参数中指定的字符大小写完全匹配时才会出现匹配。  
  
 /doc 或 /d  
 可选。 仅搜索当前文档。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。  
  
 /hidden 或 /h  
 可选。 搜索隐藏和折叠的文本，比如设计时控件的元数据、大纲文档的隐藏区域或折叠的类或方法。  
  
 /open 或 /o  
 可选。 就像一个文档一样搜索所有打开的文档。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。  
  
 /options 或 /t  
 可选。 显示当前查找选项设置的列表，并且不执行搜索。  
  
 /proc 或 /p  
 可选。 仅搜索当前过程。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。  
  
 /regex 或 /r  
 可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符，它们表示文本模式而不是文本字符。 有关正则表达式字符的完整列表，请参阅[正则表达式](../../ide/using-regular-expressions-in-visual-studio.md)。  
  
 /reset 或 /e  
 可选。 将查找选项恢复为默认设置，并且不执行搜索。  
  
 /sel 或 /s  
 可选。 仅搜索当前选择。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。  
  
 /up 或 /u  
 可选。 从文件内的当前位置向文件的顶部进行搜索。 默认情况下，搜索从文件内的当前位置开始，向文件的底部进行搜索。  
  
 /wild 或 /l  
 可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符来表示字符或字符序列。  
  
 /word 或 /w  
 可选。 只搜索全字。  
  
## <a name="example"></a>示例  
 此示例用所有打开文档中的 `btnSubmit` 替换 `btnSend`。  
  
```  
>Edit.Replace btnSend btnSubmit /open  
```  
  
## <a name="see-also"></a>另请参阅  
 [查找和替换文本](../../ide/finding-and-replacing-text.md)   
 [“命令”窗口](../../ide/reference/command-window.md)   
 [“查找/命令”框](../../ide/find-command-box.md)   
 [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)   
 [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
