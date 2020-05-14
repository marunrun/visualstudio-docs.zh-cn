---
title: 异步Task方法构建&lt;器Tresult&gt;结构 - 内部成员 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
- debug engines, AsyncTaskMethodBuilder<TResult> structure [.NET Framework]
ms.assetid: 17ebc340-8170-4aff-bf54-dc4548c83632
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c4f4da7070af09937af9e047ec83142584942e6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739331"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>异步任务方法构建&lt;器&gt;TResult 结构 - 内部成员
本主题介绍<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>类的内部成员。 有关此类的一般信息，<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>请参阅参考主题。

 **命名空间：**<xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集**：mscorlib（在 mscorlib.dll 中）

 由于您无法从 .NET 框架访问这些内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|描述|
|----------|-----------------|
|[对象 IdforDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|获取可用于唯一标识调试器此生成器的对象。|
|[m_task字段](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|表示懒惰地初始化的已生成任务。|

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>
- [.NET 框架的并行扩展内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
