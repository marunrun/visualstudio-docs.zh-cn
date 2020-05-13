---
title: 获取任务计划器调试器方法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a3b0c8c16b10a4cf2268161d8a2db96c10303b1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738643"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger 方法
检索当前处于活动状态的所有<xref:System.Threading.Tasks.TaskScheduler>对象的数组。

 **命名空间：**<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集**：mscorlib（在*mscorlib.dll*中）

 由于您无法从 .NET 框架访问此内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>返回值
 当前在此<xref:System.AppDomain>处于活动状态的所有<xref:System.Threading.Tasks.TaskScheduler>对象的数组。

## <a name="remarks"></a>备注
 此方法不安全，不应将其与其他实例同时使用<xref:System.Threading.Tasks.TaskScheduler>。 仅当调试器挂起所有其他线程时，才从调试器调用此方法。

## <a name="see-also"></a>请参阅
- [任务计划器类](../../extensibility/debugger/taskscheduler-class-internal-members.md)
