---
title: EvaluateStatement
ms.date: 02/25/2019
ms.topic: reference
f1_keywords:
- debug.evaluatestatement
helpviewer_keywords:
- Debug.EvaluateStatement command
- Evaluate Statement command
ms.assetid: 032039bc-9477-4f93-9b9d-66d4be0e90f4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7eff96d1b413ea10b1274eb7d7938148727acbc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62790871"
---
# <a name="evaluate-statement-command"></a>Evaluate Statement 命令

计算并显示给定的语句。

## <a name="syntax"></a>语法

```cmd
>Debug.EvaluateStatement text
```

## <a name="arguments"></a>自变量

`text`

必需。 要评估的语句。

## <a name="example"></a>示例

```cmd
>Debug.EvaluateStatement args.Length
```

## <a name="see-also"></a>请参阅

- [“打印”命令](../../ide/reference/print-command.md)
- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)