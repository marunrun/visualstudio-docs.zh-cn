---
title: 设置通知等待完成方法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 226ac41c8e3b7427ac3b9aba7bea08dbb7329d16
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712863"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion 方法
设置或清除TASK_STATE_WAIT_COMPLETION_NOTIFICATION状态位。

 **命名空间：**<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集**：mscorlib（在*mscorlib.dll*中）

## <a name="syntax"></a>语法

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>参数
 `enabled`

 `true`设置位;`false`取消设置位。

## <a name="exceptions"></a>例外

## <a name="remarks"></a>备注
 调试器设置此位以帮助退出异步方法体。 如果是`enabled``true`，只能对尚未完成的任务调用此方法。 何时`enabled` `false`，可以在已完成的任务上调用此方法。 在这两个事件中，它只能用于承诺样式的任务。

## <a name="requirements"></a>要求

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
