---
title: 任务计划员类 - 内部成员 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TaskScheduler class [.NET Framework debug engines]
- debug engines, TaskScheduler class [.NET Framework]
ms.assetid: 87f1c969-0217-4464-8907-7609c1bf61d3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a53abc8b24edb06445c23c19744d00d50de8735d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712567"
---
# <a name="taskscheduler-class---internal-members"></a>任务计划器类 - 内部成员
本文介绍了帮助您实现自定义调试器的<xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>类的内部成员。 有关此类的一般信息，<xref:System.Threading.Tasks.TaskScheduler>请参阅参考文章。

 **命名空间：**<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集**：mscorlib（在*mscorlib.dll*中）

 由于您无法从 .NET 框架访问这些内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler
       extends System.Object
```

## <a name="members"></a>成员

### <a name="methods"></a>方法

|名称|描述|
|----------|-----------------|
|[获取调试器的计划任务](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|检索所有计划任务的数组。|
|[获取任务计划对调试器](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|检索当前处于活动状态的所有<xref:System.Threading.Tasks.TaskScheduler>对象的数组。|

## <a name="remarks"></a>备注

## <a name="see-also"></a>请参阅
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [.NET 框架的并行扩展内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
