---
title: “设置基数”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setradix
helpviewer_keywords:
- Set Radix command
- Debug.SetRadix command
ms.assetid: 6ffd1554-7530-4da4-b5f5-e276a5034f3b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 13341d8cb6a708f4e10f211bd47b79a75e1b6e2a
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926041"
---
# <a name="set-radix-command"></a>“设置基数”命令
设置或返回用来显示整数值的数值基数。

## <a name="syntax"></a>语法

```cmd
Debug.SetRadix [10 | 16 | hex | dec]
```

## <a name="arguments"></a>自变量
`10` 或 `16` 或 `hex` 或 `dec`

可选。 指示十进制（10 或 dec）或十六进制（16 或 hex）。 如果省略某个参数，则返回当前基数值。

## <a name="example"></a>示例
此示例将环境设置为以十六进制格式显示整数值。

```cmd
>Debug.SetRadix hex
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)