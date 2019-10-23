---
title: “在文件中替换”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.replaceinfiles
helpviewer_keywords:
- Edit.ReplaceInFiles command
- Replace In Files command
- ReplaceInFiles command
ms.assetid: f116066a-4f65-4f2c-94ef-12cbd8cfb598
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fccfe696da2d38ff03ffb2f9b91de481e924a514
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748665"
---
# <a name="replace-in-files-command"></a>“在文件中替换”命令
使用“查找和替换”窗口的“在文件中替换”选项卡上的可用选项子集替换文件中的文本   。

## <a name="syntax"></a>语法

```
Edit.ReplaceinFiles findwhat replacewith [/all] [/case]
[/ext:extensions] [/keep] [/lookin:searchpath] [/options] [/regex]
[/reset] [/stop] [/sub] [/text2] [/wild] [/word]
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

/ex：`extensions`

可选。 指定要搜索的文件的文件扩展名。

/keep 或 /k

可选。 指定所有修改文件保持打开状态。

/lookin：`searchpath`

可选。 要搜索的目录。 如果路径包含空格，则将整个路径放在引号内。

/options 或 /t

可选。 显示当前查找选项设置的列表，并且不执行搜索。

/regex 或 /r

可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符，它们表示文本模式而不是文本字符。 有关正则表达式字符的完整列表，请参阅[正则表达式](../../ide/using-regular-expressions-in-visual-studio.md)。

/reset 或 /e

可选。 将查找选项恢复为默认设置，并且不执行搜索。

/stop

可选。 如果有搜索操作正在进行，请暂停当前搜索操作。 指定 `/stop` 时，替换将忽略所有其他参数。 例如，要停止当前替换，应输入以下内容：

```
>Edit.ReplaceinFiles /stop
```

/sub 或 /s

可选。 搜索在 /lookin:`searchpath` 参数中指定的目录中的子文件夹。

/text2 或 /2

可选。 在“查找结果 2”窗口中显示替换结果  。

/wild 或 /l

可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符来表示字符或字符序列。

/word 或 /w

可选。 仅搜索全字。

## <a name="example"></a>示例
此示例搜索 `btnCancel` 并将其替换为“我的 visual studio 项目”文件夹中所有 .cls 文件中的 `btnReset` 并在“查找结果 2”窗口显示替换信息  。

```
>Edit.ReplaceinFiles btnCancel btnReset /lookin:"c:/my visual studio projects" /ext:.cls /text2
```

## <a name="see-also"></a>请参阅

- [查找和替换文本](../../ide/finding-and-replacing-text.md)
- [在文件中替换](../../ide/replace-in-files.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)