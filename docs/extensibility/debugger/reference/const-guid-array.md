---
title: CONST_GUID_ARRAY |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONST_GUID_ARRAY
helpviewer_keywords:
- CONST_GUID_ARRAY structure
ms.assetid: bd55e7d8-372c-4c3e-9eed-28f6b415a5db
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c0021ef24e0cafec0119263d2c74175f0d38d784
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737636"
---
# <a name="const_guid_array"></a>CONST_GUID_ARRAY
保存 s 列表的结构`GUID`。

## <a name="syntax"></a>语法

```cpp
typedef struct tagCONST_GUID_ARRAY {
    DWORD       dwCount;
    CONST GUID* Members;
} CONST_GUID_ARRAY;
```

```csharp
public struct CONST_GUID_ARRAY {
    public uint   dwCount;
    public Guid[] Members;
}
```

## <a name="members"></a>成员
`dwCount`\
数组中的`GUID``Members`s 数。

`Members`\
s`GUID`数组。

## <a name="remarks"></a>备注
此结构传递给[发布程序](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)方法，并从[获取提供程序处理数据和](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) [WatchForProvider 事件](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)方法返回。

此结构实例的所有者负责释放分配的任何内存。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
