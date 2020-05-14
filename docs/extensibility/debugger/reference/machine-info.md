---
title: MACHINE_INFO |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714554"
---
# <a name="machine_info"></a>MACHINE_INFO
描述特定计算机。

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
 [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)枚举中的标志的组合，用于指定初始化结构的字段。

 `bstrName`\
 机器名称。 等效于调用[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)。

 `Flags`\
 描述计算机属性[MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md)枚举的标志的组合。

## <a name="remarks"></a>备注
 此结构通过调用[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)方法返回。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
