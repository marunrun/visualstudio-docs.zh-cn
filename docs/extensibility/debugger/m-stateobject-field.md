---
title: m_stateObject 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 95947a1367ea1ddf4aa88689f731971d5c7d0a6c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330831"
---
# <a name="mstateobject-field"></a>m_stateObject 字段
一个对象，表示该操作将使用的数据。

 **Namespace**：<xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：** mscorlib (在*mscorlib.dll*)

 无法从.NET Framework 来访问此内部成员，因为以下语法提供通用中间语言 (CIL)。

## <a name="syntax"></a>语法

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>备注
 这是`state`中的参数<xref:System.Threading.Tasks.Task.%23ctor%2A>构造函数。 它也是为支持字段<xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName>属性。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)