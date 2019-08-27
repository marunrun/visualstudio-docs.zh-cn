---
title: TASK_STATE_FAULTED 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_FAULTED field, Task class [.NET Framework debug engines]
ms.assetid: ced826ae-09a9-4acf-af00-a2343d396bb8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f8ae3c654518ec051d3f4d1fd0eeb43b4ef5e710
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348365"
---
# <a name="taskstatefaulted-field"></a>TASK_STATE_FAULTED 字段
由于未处理异常的原因而完成的任务。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_FAULTED = int32(0x00400000)
```

## <a name="remarks"></a>备注
 如果[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)字段包含此值，<xref:System.Threading.Tasks.Task.Status%2A>属性返回<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)