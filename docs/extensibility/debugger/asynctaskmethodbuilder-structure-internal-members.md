---
title: 异步Task方法构建器结构 - 内部成员 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncTaskMethodBuilder structure [.NET Framework]
- AsyncTaskMethodBuilder structure [.NET Framework debug engines]
ms.assetid: f32f5857-7ef8-45fd-8b5a-7f644eb98b11
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c918890551515ab9fadbf329d4c3ee96621c7aae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739370"
---
# <a name="asynctaskmethodbuilder-structure---internal-members"></a>异步Task方法构建器结构 - 内部成员
本主题介绍<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>类的内部成员。 有关此类的一般信息，<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>请参阅参考主题。

 **命名空间：**<xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集**：mscorlib（在 mscorlib.dll 中）

 由于您无法从 .NET 框架访问这些内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|描述|
|----------|-----------------|
|[对象 IdforDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-objectidfordebugger-property.md)|获取可用于唯一标识调试器此生成器的对象。|
|[m_builder字段](../../extensibility/debugger/asynctaskmethodbuilder-m-builder-field.md)|表示此非泛型实例委托给的泛型生成器对象。|

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>
- [.NET 框架的并行扩展内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
