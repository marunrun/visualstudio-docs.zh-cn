---
title: TaskScheduler 类-内部成员 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TaskScheduler class [.NET Framework debug engines]
- debug engines, TaskScheduler class [.NET Framework]
ms.assetid: 87f1c969-0217-4464-8907-7609c1bf61d3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 865e12819a5e7325886c0f7f5d8425a6b3d2e393
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331330"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler 类-内部成员
本文介绍的内部成员的<xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>类，可帮助您实现自定义调试器。 有关此类的常规信息，请参阅<xref:System.Threading.Tasks.TaskScheduler>参考文章。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问这些内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```csharp
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler
       extends System.Object
```

## <a name="members"></a>成员

### <a name="methods"></a>方法

|名称|描述|
|----------|-----------------|
|[GetScheduledTasksForDebugger](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|检索所有计划任务的数组。|
|[GetTaskSchedulersForDebugger](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|检索的所有数组<xref:System.Threading.Tasks.TaskScheduler>当前处于活动状态的对象。|

## <a name="remarks"></a>备注

## <a name="see-also"></a>请参阅
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)