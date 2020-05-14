---
title: .NET 框架的并行扩展内部 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6a3583e94a0bfff4474db03aa9d083add921f3da
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738270"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>.NET 框架的并行扩展内部
本节介绍内部类型、方法和类字段，这些类可帮助您实现对 .NET 框架的并行扩展的自定义调试器。

## <a name="in-this-section"></a>在本节中
 [任务类](../../extensibility/debugger/task-class-internal-members.md)描述<xref:System.Threading.Tasks.Task?displayProperty=fullName>类的内部数据成员。

 [任务计划器类](../../extensibility/debugger/taskscheduler-class-internal-members.md)描述<xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>类的内部数据成员。

 [或有属性类](../../extensibility/debugger/contingentproperties-class-internal-members.md)描述`System.Threading.Tasks.ContingentProperties`类的内部数据成员。

 [异步任务方法构建器结构](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md)描述<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>结构的内部成员。

 [异步任务方法构建\<器 TResult>结构](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md)描述<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>结构的内部成员。

 [异步VoidMethodBuilder结构](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md)描述<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>结构的内部成员。

## <a name="see-also"></a>请参阅
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [可视化工作室调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [并行编程](/dotnet/standard/parallel-programming/index)
