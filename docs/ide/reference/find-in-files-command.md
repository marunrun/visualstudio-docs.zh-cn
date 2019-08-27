---
title: “在文件中查找”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.findinfiles
helpviewer_keywords:
- Edit.FindInFiles command
- find in files command
ms.assetid: 2fc78bfe-b339-4599-97f9-4cafd8a194d9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2877057f32ba6553a2cdcefbbc1bb7a8bf2884da
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919258"
---
# <a name="find-in-files-command"></a>“在文件中查找”命令
若要搜索文件，请使用“查找和替换”  窗口的“在文件中查找”  选项卡上的可用选项子集。

## <a name="syntax"></a>语法

```cmd
Edit.FindinFiles findwhat [/case] [/ext:extensions]
[/lookin:searchpath] [/names] [/options] [/reset] [/stop] [/sub]
[/text2] [/wild|/regex] [/word]
```

## <a name="arguments"></a>自变量

`findwhat`\
必需。 要匹配的文本。

## <a name="switches"></a>开关
/case 或 /c\
可选。 仅当大小写字符和 `findwhat` 参数中指定的字符大小写完全匹配时才会出现匹配。

/ext: `extensions`\
可选。 指定要搜索的文件的文件扩展名。 如果未指定，则使用以前输入的扩展名（如果输入过）。

/lookin: `searchpath`\
可选。 要搜索的目录。 如果路径包含空格，则将整个路径放在引号内。

/names 或 /n\
可选。 显示包含匹配项的文件名列表。

/options 或 /t\
可选。 显示当前查找选项设置的列表，并且不执行搜索。

/regex 或 /r\
可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符，它们表示文本模式而不是文本字符。 有关正则表达式字符的完整列表，请参阅[正则表达式](../../ide/using-regular-expressions-in-visual-studio.md)。

/reset 或 /e\
可选。 将查找选项恢复为默认设置，并且不执行搜索。

/stop\
可选。 如果有搜索操作正在进行，请暂停当前搜索操作。 指定 `/stop` 时，搜索会忽略所有其他参数。 例如，若要停止当前搜索，应输入以下内容：

```cmd
>Edit.FindinFiles /stop
```

/sub 或 /s\
可选。 搜索在 /lookin:`searchpath` 参数中指定的目录中的子文件夹。

/text2 或 /2\
可选。 在“查找结果 2”窗口中显示搜索结果。

/wild 或 /l\
可选。 使用在 `findwhat` 参数中作为表示形式进行预定义的特殊字符来表示字符或字符序列。

/word 或 /w\
可选。 只搜索全字。

## <a name="example"></a>示例
此示例在位于“我的 Visual Studio 项目”文件夹下的所有 .cls 文件中搜索 btnCancel，并在“查找结果 2”窗口中显示匹配信息。

```cmd
>Edit.FindinFiles btnCancel /lookin:"c:/My Visual Studio Projects" /ext:*.cls /text2
```

## <a name="see-also"></a>另请参阅

- [在文件中查找](../../ide/find-in-files.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)