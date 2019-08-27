---
title: “查找”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.find
helpviewer_keywords:
- Find command
- Edit.Find command
ms.assetid: f0c705dc-2b97-423d-abbf-5584d4827208
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9e94f8aa823fc7665144f1d774339d1c41f37edc
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926241"
---
# <a name="find-command"></a>“查找”命令
要搜索文件，请使用“查找和替换”窗口的“在文件中查找”选项卡上的可用选项子集   。

## <a name="syntax"></a>语法

```cmd
Edit.Find findwhat [/case] [/doc | /proc | /open | /sel]
[/markall] [/options] [/reset] [/up] [/wild | /regex] [/word]
```

## <a name="arguments"></a>自变量
`findwhat`（必需）。 要匹配的文本。

## <a name="switches"></a>开关
/case 或 /c\
可选。 仅当大小写字符和 `findwhat` 参数中指定的字符大小写完全匹配时才会出现匹配。

/doc 或 /d\
可选。 仅搜索当前文档。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。

/markall 或 /m\
可选。 在每一行上放置一个图形，该行包含当前文档中的搜索匹配项。

/open 或 /o\
可选。 就像一个文档一样搜索所有打开的文档。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。

/options 或 /t\
可选。 显示当前查找选项设置的列表，并且不执行搜索。

/proc 或 /p\
可选。 仅搜索当前过程。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。

/reset 或 /e\
可选。 将查找选项恢复为默认设置，并且不执行搜索。

/sel 或 /s\
可选。 仅搜索当前选择。 仅指定一个可用搜索范围，`/doc`、`/proc`、`/open` 或 `/sel`。

/up 或 /u\
可选。 从文件中的当前位置向文件开始位置搜索。 默认情况下，搜索从文件内的当前位置开始，向文件的结尾处搜索。

/regex 或 /r\
可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符，它们表示文本模式而不是文本字符。 有关正则表达式字符的完整列表，请参阅[正则表达式](../../ide/using-regular-expressions-in-visual-studio.md)。

/wild 或 /l\
可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符来表示字符或字符序列。

/word 或 /w\
可选。 只搜索全字。

## <a name="example"></a>示例
此示例在当前选中代码部分搜索“somestring”，需要区分大小写。

```cmd
>Edit.Find somestring /sel /case
```

## <a name="see-also"></a>另请参阅

- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)