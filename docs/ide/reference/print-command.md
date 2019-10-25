---
title: Debug.Print
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae87afb11be71af8f0582a0b2899d67ba970186e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747826"
---
# <a name="print-command"></a>“打印”命令

计算表达式或显示指定文本。

## <a name="syntax"></a>语法

```cmd
>Debug.Print text
```

## <a name="arguments"></a>自变量

`text`

必需。 要计算的表达式或要显示的文本。

## <a name="remarks"></a>备注

可使用问号 (?) 作为此命令的别名。 例如，命令

```cmd
>Debug.Print expA
```

也可写作

```cmd
? expA
```

此命令的这两个版本都会返回表达式 `expA` 的当前值。

## <a name="example"></a>示例

```cmd
>Debug.Print DateTime.Now.Day
```

## <a name="see-also"></a>请参阅

- [“计算语句”命令](../../ide/reference/evaluate-statement-command.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)