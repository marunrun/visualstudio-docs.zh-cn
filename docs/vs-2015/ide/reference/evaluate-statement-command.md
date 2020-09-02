---
title: “计算语句”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.evaluatestatement
helpviewer_keywords:
- Debug.EvaluateStatement command
- Evaluate Statement command
ms.assetid: 032039bc-9477-4f93-9b9d-66d4be0e90f4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6e2db8596c1c16f5c9fb54a8c7c867b06e997b7b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657713"
---
# <a name="evaluate-statement-command"></a>“计算语句”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

计算并显示给定的语句。

## <a name="syntax"></a>语法

```
Debug.EvaluateStatement text
```

## <a name="arguments"></a>参数
 `text`（必需）。 要评估的语句。

## <a name="remarks"></a>备注
 用于输入 EvaluateStatement 命令的窗口确定是将等号 (=) 解释为比较运算符还是赋值运算符****。

 在“命令”窗口中，将等号 (=) 解释为比较运算符****。 例如，如果变量 `a` 和 `b` 的值不同，则命令

```
>Debug.EvaluateStatement(a=b)
```

 将返回 `false` 的值。

 与此相反，在“即时”窗口中，将等号 (=) 解释为赋值运算符****。 例如，命令

```
>Debug.EvaluateStatement(a=b)
```

 将为变量 `a` 赋予变量 `b` 的值。

## <a name="example"></a>示例

```
>Debug.EvaluateStatement(a+b)
```

## <a name="see-also"></a>另请参阅
 [打印命令](../../ide/reference/print-command.md) [visual Studio 命令](../../ide/reference/visual-studio-commands.md)[命令窗口](../../ide/reference/command-window.md)[查找/命令框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
