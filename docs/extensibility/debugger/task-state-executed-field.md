---
title: TASK_STATE_EXECUTED 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_EXECUTED field, Task class [.NET Framework debug engines]
ms.assetid: 75b8f9d0-b908-40d0-b109-70feaed2ab0c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa637b8bc29f53ca6dde1b13310d83a5e176408f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80712704"
---
# <a name="task_state_executed-field"></a>TASK_STATE_EXECUTED 字段
该任务正在运行，但尚未完成。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (mscorlib.dll) 

 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_EXECUTED = int32(0x00020000)
```

## <a name="remarks"></a>备注
 如果 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md) 字段包含此值，则 <xref:System.Threading.Tasks.Task.Status%2A> 属性将返回 <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> 。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
