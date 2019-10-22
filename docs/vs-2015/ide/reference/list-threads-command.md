---
title: “列出线程”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listthreads
helpviewer_keywords:
- ListThreads command
- list threads command
- Debug.ListThreads command
ms.assetid: 34b665c0-d46f-4c1a-a066-b678eba5ac54
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fc11479901785b19235e0962d3ae90e552e5b33b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671138"
---
# <a name="list-threads-command"></a>“列出线程”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示当前程序中线程的列表。

## <a name="syntax"></a>语法

```
Debug.ListThreads [index]
```

## <a name="arguments"></a>自变量
 `index`（可选）。 通过索引来选择要用作当前线程的线程。

## <a name="remarks"></a>备注
 如果已指定，`index` 实际参数将指示的线程标记为当前线程。 星号 (*) 显示在当前线程旁边的列表中。

## <a name="example"></a>示例

```
>Debug.ListThreads
```

## <a name="see-also"></a>另请参阅
 "[列出调用堆栈" 命令](../../ide/reference/list-call-stack-command.md)[列表反汇编命令](../../ide/reference/list-disassembly-command.md) [visual studio 命令](../../ide/reference/visual-studio-commands.md)[命令窗口](../../ide/reference/command-window.md)[查找/命令框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
