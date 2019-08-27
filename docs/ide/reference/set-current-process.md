---
title: 设置当前进程
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Debug.SetCurrentProcess command
- Set Current Process command
ms.assetid: 1e016ebd-aadd-411f-a606-03bf69d3f8aa
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8d4c23934ddb6a838344eb6252f6002a5ecf10d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926090"
---
# <a name="set-current-process"></a>设置当前进程
将指定的进程设置为调试器中的活动进程。

## <a name="syntax"></a>语法

```cmd
Debug.SetCurrentProcess index
```

## <a name="arguments"></a>自变量
`index`

必需。 进程的索引。

## <a name="remarks"></a>备注
调试时可以附加到多个进程，但在任何给定时间，调试器中只有一个进程处于活动状态。 可以使用 `SetCurrentProcess` 命令设置活动进程。

## <a name="example"></a>示例

```cmd
>Debug.SetCurrentProcess 1
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 命令](../../ide/reference/visual-studio-commands.md)
- [“命令”窗口](../../ide/reference/command-window.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)