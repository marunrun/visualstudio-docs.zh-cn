---
title: “设置当前堆栈帧”命令 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setcurrentstackframe
helpviewer_keywords:
- Set Current Stack Frame command
- Debug.SetCurrentStackFrame command
ms.assetid: 3dcf52c0-6781-4598-bac2-0094dce67c20
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4fcb38e565ea4f30ed6e669f8b98df09c9d733ea
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665459"
---
# <a name="set-current-stack-frame-command"></a>“设置当前堆栈帧”命令
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

允许设置特定堆栈帧。

## <a name="syntax"></a>语法

```
Debug.SetCurrentStackFrame index
```

## <a name="arguments"></a>自变量
 `index`（必需）。 通过其索引选择堆栈帧。

## <a name="example"></a>示例

```
>Debug.SetCurrentStackFrame 1
```

## <a name="see-also"></a>另请参阅
 [Visual studio](../../ide/reference/visual-studio-commands.md) "[命令" 窗口](../../ide/reference/command-window.md)中的["查找/命令" 框](../../ide/find-command-box.md) [visual studio 命令别名](../../ide/reference/visual-studio-command-aliases.md)
