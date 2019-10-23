---
title: “设置当前堆栈帧”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setcurrentstackframe
helpviewer_keywords:
- Set Current Stack Frame command
- Debug.SetCurrentStackFrame command
ms.assetid: 3dcf52c0-6781-4598-bac2-0094dce67c20
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 088fe9871b54e69b015ffdc9dcdaf23de3d98e0e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747761"
---
# <a name="set-current-stack-frame-command"></a>“设置当前堆栈帧”命令
允许设置特定堆栈帧。

## <a name="syntax"></a>语法

```cmd
Debug.SetCurrentStackFrame index
```

## <a name="arguments"></a>自变量
`index`

必需。 通过其索引选择堆栈帧。

## <a name="example"></a>示例

```cmd
>Debug.SetCurrentStackFrame 1
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)