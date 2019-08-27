---
title: PROVIDER_PROCESS_DATA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_PROCESS_DATA
helpviewer_keywords:
- PROVIDER_PROCESS_DATA structure
ms.assetid: ec2362ed-4a0c-4a09-9d66-8ff04e4f41ee
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 18b60d68b8c36c1d0c4fcd2a90e25732108460ee
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347243"
---
# <a name="providerprocessdata"></a>PROVIDER_PROCESS_DATA
此结构可提供有关计算机上运行的进程的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct tagPROVIDER_PROCESS_DATA {
   PROVIDER_FIELDS    Fields;
   PROGRAM_NODE_ARRAY ProgramNodes;
   BOOL               fIsDebuggerPresent;
} PROVIDER_PROCESS_DATA;
```

```csharp
public struct PROVIDER_PROCESS_DATA {
   public uint               Fields;
   public PROGRAM_NODE_ARRAY ProgramNodes;
   public int                fIsDebuggerPresent;
}
```

## <a name="members"></a>成员
 `Fields`\
 中的标志的组合[PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)指示填充的字段的枚举。

 `ProgramNodes`\
 一个[PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)结构，其中包含程序节点的数组。

 `fIsDebuggerPresent`\
 非零值 (`TRUE`) 如果[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试器正在运行，零 (`FALSE`) 如果不是。

## <a name="remarks"></a>备注
 此结构传递给[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)填写其中的方法。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)
- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)