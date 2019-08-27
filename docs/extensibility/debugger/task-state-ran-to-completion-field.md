---
title: TASK_STATE_RAN_TO_COMPLETION 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_RAN_TO_COMPLETION field, Task class [.NET Framework debug engines]
ms.assetid: 0f4830af-fe0c-4141-b768-817f4e426b8c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6a7108a9f17ee308c781e652fddc2c0fc6277e1d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331430"
---
# <a name="taskstaterantocompletion-field"></a>TASK_STATE_RAN_TO_COMPLETION 字段
已成功完成执行的任务。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_RAN_TO_COMPLETION = int32(0x02000000)
```

## <a name="remarks"></a>备注
 如果[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)字段包含此值，<xref:System.Threading.Tasks.Task.Status%2A>属性返回<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)