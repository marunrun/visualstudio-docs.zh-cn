---
title: PROVIDER_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FIELDS
helpviewer_keywords:
- PROVIDER_FIELDS enumeration
ms.assetid: 39631545-2b0e-45b4-978b-d63656484b02
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 923ae0bc3ca03dabee7b5d4bca74d24c7f7d5815
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329371"
---
# <a name="providerfields"></a>PROVIDER_FIELDS
指定与程序提供程序关联的属性。

## <a name="syntax"></a>语法

```cpp
enum enum_PROVIDER_FIELDS {
   PFIELD_PROGRAM_NODES       = 0x01,
   PFIELD_IS_DEBUGGER_PRESENT = 0x02
};
typedef DWORD PROVIDER_FIELDS;
```

```csharp
public enum enum_PROVIDER_FIELDS {
   PFIELD_PROGRAM_NODES       = 0x01,
   PFIELD_IS_DEBUGGER_PRESENT = 0x02
};
```

## <a name="fields"></a>字段
 `PFIELD_PROGRAM_NODES`\
 `ProgramNodes`字段才有效。

 `PFIELD_IS_DEBUGGER_PRESENT`\
 `fIsDebuggerPresent`字段才有效。

## <a name="remarks"></a>备注
 这些值中返回`Fields`的成员[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)结构，以指示已显式填充结构的哪些字段。

 可以组合这些值的按位`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)