---
title: 通知调试等待完成方法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8963e29a067754c0e8c89b9db336b239ac682ce1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738329"
---
# <a name="notifydebuggerofwaitcompletion-method"></a>通知调试等待完成方法
占位符方法用作调试器的断点目标。 此方法不能内联或优化。

 **命名空间：**<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集**：mscorlib（在*mscorlib.dll*中）

## <a name="syntax"></a>语法

```vb
private void NotifyDebuggerOfWaitCompletion()
```

## <a name="remarks"></a>备注
 如果设置了具有任务的调试器通知位，则所有具有任务的联接操作都应调用此方法。

## <a name="requirements"></a>要求

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
