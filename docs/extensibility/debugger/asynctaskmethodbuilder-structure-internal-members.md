---
title: AsyncTaskMethodBuilder 结构-内部成员 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncTaskMethodBuilder structure [.NET Framework]
- AsyncTaskMethodBuilder structure [.NET Framework debug engines]
ms.assetid: f32f5857-7ef8-45fd-8b5a-7f644eb98b11
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f080e7a0fef7a03b878c253f09661338b5704df
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317634"
---
# <a name="asynctaskmethodbuilder-structure---internal-members"></a>AsyncTaskMethodBuilder 结构-内部成员
本主题介绍的内部成员的<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>类。 有关此类的常规信息，请参阅<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>参考主题。

 **Namespace**：<xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集：** mscorlib （在 mscorlib.dll 中)

 无法从.NET Framework 来访问这些内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|描述|
|----------|-----------------|
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-objectidfordebugger-property.md)|获取可用于唯一地标识调试器到此生成器的对象。|
|[m_builder 字段](../../extensibility/debugger/asynctaskmethodbuilder-m-builder-field.md)|表示此非泛型实例委托的泛型生成器对象。|

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>
- [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)