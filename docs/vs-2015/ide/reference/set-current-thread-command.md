---
title: “设置当前线程”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setcurrentthread
helpviewer_keywords:
- Set Current Thread command
- Debug.SetCurrentThread command
ms.assetid: 9917ed1d-6c30-4d94-b2f0-69acce74f1b2
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67bf0d37e6f734fa4b3229488bc3eee2732c3063
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665447"
---
# <a name="set-current-thread-command"></a>“设置当前线程”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将指定的线程设置为当前线程。

## <a name="syntax"></a>语法

```
Debug.SetCurrentThread index
```

## <a name="arguments"></a>自变量
 `index`（必需）。 按线程的索引选择线程。

## <a name="example"></a>示例

```
>Debug.SetCurrentThread 1
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) "[命令" 窗口](../../ide/reference/command-window.md)中的["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
