---
title: m_children 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab6446b18350fe1f11e0b164d9eb4bff39035ddb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330894"
---
# <a name="mchildren-field"></a>m_children field
使用此任务中注册的子任务的列表。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>备注
 运行任务时，只有执行任务的线程应访问此数组。

 如果完成此任务，其他线程可以访问此字段，只要它们不将任何内容添加到其中或从中删除任何内容。

## <a name="see-also"></a>请参阅
- [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md)