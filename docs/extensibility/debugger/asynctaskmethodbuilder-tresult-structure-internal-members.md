---
title: AsyncTaskMethodBuilder &lt; TResult &gt; 结构-内部成员 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739331"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>AsyncTaskMethodBuilder &lt; TResult &gt; 结构-内部成员
本主题介绍类的内部成员 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 。 有关此类的常规信息，请参阅 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 参考主题。

 **命名空间：** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **Assembly：** mscorlib (mscorlib.dll) 

 由于无法从 .NET Framework 访问这些内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|说明|
|----------|-----------------|
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|获取一个对象，该对象可用于将此生成器唯一标识到调试器。|
|[m_task 字段](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|表示延迟初始化的生成任务。|

## <a name="see-also"></a>另请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>
- [.NET Framework 的并行扩展内部机制](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
