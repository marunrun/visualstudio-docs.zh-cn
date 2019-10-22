---
title: 设置当前进程 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Debug.SetCurrentProcess command
- Set Current Process command
ms.assetid: 1e016ebd-aadd-411f-a606-03bf69d3f8aa
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c362d3f5dda5015e91ac88dd8f0abd60a185ba72
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665467"
---
# <a name="set-current-process"></a>设置当前进程
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将指定的进程设置为调试器中的活动进程。

## <a name="syntax"></a>语法

```
Debug.SetCurrentProcess index
```

## <a name="arguments"></a>自变量
 `index`（必需）。 进程的索引。

## <a name="remarks"></a>备注
 调试时可以附加到多个进程，但在任何给定时间，调试器中只有一个进程处于活动状态。 可以使用 `SetCurrentProcess` 命令设置活动进程。

## <a name="example"></a>示例

```
>Debug.SetCurrentProcess 1
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) "命令"[窗口](../../ide/reference/command-window.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
