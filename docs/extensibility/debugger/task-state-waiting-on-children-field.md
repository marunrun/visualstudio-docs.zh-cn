---
title: TASK_STATE_WAITING_ON_CHILDREN 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_WAITING_ON_CHILDREN field, Task class [.NET Framework debug engines]
ms.assetid: 6f26b098-84ad-4f6e-ba27-6136581ba630
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ae7f7930161b07dc8aeb4f3ff8bfb506e9f6e737
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345393"
---
# <a name="taskstatewaitingonchildren-field"></a>TASK_STATE_WAITING_ON_CHILDREN 字段
任务已完成执行其委托，隐式等待附加的子任务完成。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_WAITING_ON_CHILDREN = int32(0x01000000)
```

## <a name="remarks"></a>备注
 如果[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)字段包含此值，<xref:System.Threading.Tasks.Task.Status%2A>属性返回<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)