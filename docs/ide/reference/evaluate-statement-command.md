---
title: EvaluateStatement
description: 了解 Evaluate Statement 命令，以及它如何计算并显示给定语句。
ms.custom: SEO-VS-2020
ms.date: 02/25/2019
ms.topic: reference
f1_keywords:
- debug.evaluatestatement
helpviewer_keywords:
- Debug.EvaluateStatement command
- Evaluate Statement command
ms.assetid: 032039bc-9477-4f93-9b9d-66d4be0e90f4
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 264629769bbb25af97404e7c97c2676c4951f8d3
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305431"
---
# <a name="evaluate-statement-command"></a>“计算语句”命令

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
- [Visual Studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
