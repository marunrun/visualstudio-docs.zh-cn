---
title: 异步任务方法构建&lt;器&gt;Tresult .m_task 字段 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_task field, AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
ms.assetid: 649abf0e-0fec-49d9-93b2-8953521f7ba5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 43822417a000a51b11c18e282860dc0dbfb08332
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739367"
---
# <a name="asynctaskmethodbuilderlttresultgtm_task-field"></a>异步任务方法生成器&lt;Tresult&gt;.m_task 字段
表示懒惰地初始化的已生成任务。

 **命名空间：**<xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **程序集**：mscorlib（在 mscorlib.dll 中）

 由于您无法从 .NET 框架访问此内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.field private class System.Threading.Tasks.Task`1<!TResult> m_task
```

## <a name="see-also"></a>请参阅
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>
- [.NET 框架的并行扩展内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
