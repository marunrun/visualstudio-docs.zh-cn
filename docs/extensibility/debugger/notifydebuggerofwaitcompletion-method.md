---
title: NotifyDebuggerOfWaitCompletion 方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9a3280a24ad7f9d4045c9a1bff6ca2b44c724325
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350639"
---
# <a name="notifydebuggerofwaitcompletion-method"></a>NotifyDebuggerOfWaitCompletion 方法
由调试器使用断点目标的占位符方法。 此方法不能内联或优化。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

## <a name="syntax"></a>语法

```vb
private void NotifyDebuggerOfWaitCompletion()
```

## <a name="remarks"></a>备注
 与任务的所有联接操作应都调用此方法，如果其调试器通知位设置。

## <a name="requirements"></a>要求

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)