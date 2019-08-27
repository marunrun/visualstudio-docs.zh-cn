---
title: MACHINE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO
helpviewer_keywords:
- MACHINE_INFO structure
ms.assetid: e7564ff2-00b5-4750-8fd5-dc1029a16912
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e50fe4901ebcbf008bf191226502ccac8ec4cf5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339223"
---
# <a name="machineinfo"></a>MACHINE_INFO
描述某一特定计算机。

## <a name="syntax"></a>语法

```cpp
typedef struct tagMACHINE_INFO { 
   MACHINE_INFO_FIELDS Fields;
   BSTR                bstrName;
   MACHINE_INFO_FLAGS  Flags;
} MACHINE_INFO;
```

```csharp
public struct MACHINE_INFO { 
   public uint   Fields;
   public string bstrName;
   public uint   Flags;
};
```

## <a name="members"></a>成员
 `Fields`\
 中的标志的组合[MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)枚举，用于指定结构的哪些字段进行初始化。

 `bstrName`\
 计算机名称。 等效于调用[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)。

 `Flags`\
 中的标志的组合[MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md)描述计算机属性的枚举。

## <a name="remarks"></a>备注
 此结构返回通过调用[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)方法。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)