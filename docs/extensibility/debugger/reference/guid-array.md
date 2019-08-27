---
title: GUID_ARRAY | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GUID_ARRAY structure
ms.assetid: 9e12500c-2c1c-49b1-a0ba-e08366c97eb8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d53413ee56700fe39470d3bbc3229f4b8b668373
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317530"
---
# <a name="guidarray"></a>GUID_ARRAY
介绍可用的调试引擎的唯一标识符的数组。

## <a name="syntax"></a>语法

```cpp
typedef struct tagGUID_ARRAY
{
    DWORD dwCount;
    GUID *Members;
} GUID_ARRAY;
```

```csharp
public struct GUID_ARRAY
{
    public uint dwCount;
    public Guid Members;
}
```

## <a name="members"></a>成员
`dwCount`\
数组中的唯一标识符的数量。

`Members`\
数组，其中包含唯一标识符。

## <a name="remarks"></a>备注
返回此结构[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)方法。

## <a name="requirements"></a>要求
标头：Msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)
