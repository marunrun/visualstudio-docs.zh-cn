---
title: SetNotificationForWaitCompletion 方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5d9bee2579cc3a93f657291551955f0c9b7565b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348587"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion 方法
设置或清除 TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状态位。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

## <a name="syntax"></a>语法

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>参数
 `enabled`

 `true` 若要设置的位;`false`取消设置了位。

## <a name="exceptions"></a>Exceptions

## <a name="remarks"></a>备注
 调试器设置此位，以帮助脱离异步方法正文。 如果`enabled`是`true`，必须仅在尚未完成的任务上调用此方法。 当`enabled`是`false`，可以在已完成的任务上调用此方法。 在既情况下，它应仅用于承诺样式任务。

## <a name="requirements"></a>要求

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)