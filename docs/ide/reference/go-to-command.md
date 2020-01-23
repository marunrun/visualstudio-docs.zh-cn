---
title: “转到”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.goto
helpviewer_keywords:
- Debug.Goto command
- Go To command
ms.assetid: 201e1dd2-6701-467d-8cc1-faec2ef20511
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 535906d8b8d7f8ba0c2984d22ceead18a0d47c2d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75569200"
---
# <a name="go-to-command"></a>“转到”命令
将光标移到指定的行。

## <a name="syntax"></a>语法

```cmd
Edit.GoTo [linenumber]
```

## <a name="arguments"></a>自变量
`linenumber`\
可选。 一个表示要转到的行号的整数。

## <a name="remarks"></a>备注
行号从 1 开始。 如果 `linenumber` 的值小于 1，则显示第一行。 如果 `linenumber` 的值大于最后一行的行号，则显示最后一行。

如果未指定 `linenumber` 的值，则显示“转到行”对话框  。

此命令的别名为 GoToLn。

## <a name="example"></a>示例

```cmd
>Edit.GoTo 125
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
