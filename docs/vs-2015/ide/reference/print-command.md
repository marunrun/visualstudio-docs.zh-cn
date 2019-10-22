---
title: Print 命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 136edf7fa91e4caeb9303edfd4441ee178fa6038
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662157"
---
# <a name="print-command"></a>Print 命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

计算表达式或显示指定文本。

## <a name="syntax"></a>语法

```
Debug.Print text
```

## <a name="arguments"></a>自变量
 `text`（必需）。 要计算的表达式或要显示的文本。

## <a name="remarks"></a>备注
 可使用问号 (?) 作为此命令的别名。 例如，命令

```
>Debug.Print expA
```

 也可写作

```
>? expA
```

 此命令的这两个版本都将返回表达式 `expA` 的当前值。

## <a name="example"></a>示例

```
>Debug.Print varA
```

## <a name="see-also"></a>另请参阅
 "[计算语句" 命令](../../ide/reference/evaluate-statement-command.md) [Visual Studio](../../ide/reference/visual-studio-commands.md)命令[窗口](../../ide/reference/command-window.md) ["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
