---
title: m_children字段 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 07933fd4c9f359e72714600abdf8b4ee29268f84
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738423"
---
# <a name="m_children-field"></a>m_children字段
在此任务中注册的子任务的列表。

 **命名空间：**<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集**：mscorlib（在*mscorlib.dll*中）

 由于您无法从 .NET 框架访问此内部成员，因此在通用中间语言 （CIL） 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>备注
 当任务运行时，只有执行该任务的线程应访问此数组。

 如果任务已完成，则其他线程可以访问此字段，只要它们不向该字段添加任何内容或从中删除任何内容。

## <a name="see-also"></a>请参阅
- [或有属性类](../../extensibility/debugger/contingentproperties-class-internal-members.md)
