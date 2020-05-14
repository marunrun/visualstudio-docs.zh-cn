---
title: 异步虚无方法构建器结构 - 内部成员 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncVoidMethodBuilder structure [.NET Framework]
- AsyncVoidMethodBuilder structure [.NET Framework debug engines]
ms.assetid: fe2970ab-d4c5-4355-a8e4-772ee0a57178
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 866a53fae7bb2cc5325112b84d992da6f95af246
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739299"
---
# <a name="asyncvoidmethodbuilder-structure---internal-members"></a>异步VoidMethodBuilder结构 - 内部成员
本主题介绍<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>类的内部成员。 有关此类的一般信息，<xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>请参阅参考主题。

 **命名空间：**<xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集**：mscorlib（在 mscorlib.dll 中）

 由于您无法从 .NET 框架访问这些内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncVoidMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>内部成员

|名称|描述|
|----------|-----------------|
|[对象 IdforDebugger 属性](../../extensibility/debugger/asyncvoidmethodbuilder-objectidfordebugger-property.md)|获取可用于唯一标识调试器此生成器的对象。|
|[m_objectIdForDebugger字段](../../extensibility/debugger/asyncvoidmethodbuilder-m-objectidfordebugger-field.md)|表示调试器用于唯一标识此生成器的懒惰初始化对象。|

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>
- [.NET 框架的并行扩展内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
