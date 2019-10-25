---
title: “启动”命令
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.start
helpviewer_keywords:
- Start command
- Debug.Start command
ms.assetid: dc4e4aa2-b0ab-4e00-92db-6dc3058ddc21
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6f3179c223aef8226577fe726b6d91301d42572a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748633"
---
# <a name="start-command"></a>“启动”命令
开始调试启动项目。

## <a name="syntax"></a>语法

```cmd
Debug.Start [address]
```

## <a name="arguments"></a>自变量
`address`

可选。 程序挂起执行的地址，类似于源代码中的断点。 此参数仅在调试模式下有效。

## <a name="remarks"></a>备注
“启动”命令在执行时会对指定的地址执行 RunToCursor 操作  。

## <a name="example"></a>示例
此示例启动调试器并忽略任何发生的异常。

```cmd
>Debug.Start
```

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [“查找/命令”框](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)