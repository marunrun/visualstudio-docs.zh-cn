---
title: MACHINE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO
helpviewer_keywords:
- MACHINE_INFO structure
ms.assetid: e7564ff2-00b5-4750-8fd5-dc1029a16912
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad66992bd07afa2ef563c1b58fab0172e9a6121e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80714554"
---
# <a name="machine_info"></a>MACHINE_INFO
描述特定的计算机。

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
 [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)枚举中的标志的组合，用于指定要初始化结构的哪些字段。

 `bstrName`\
 计算机名称。 等效于调用 [GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)。

 `Flags`\
 描述计算机特性的 [MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md) 枚举中的标志的组合。

## <a name="remarks"></a>备注
 此结构由对 [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md) 方法的调用返回。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
