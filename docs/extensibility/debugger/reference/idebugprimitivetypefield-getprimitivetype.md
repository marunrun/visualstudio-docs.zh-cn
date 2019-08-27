---
title: IDebugPrimitiveTypeField::GetPrimitiveType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetPrimitiveType
- IDebugPrimitiveTypeField::GetPrimitiveType
ms.assetid: a186c922-bbfe-478c-a744-b21eb4672d8f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0eed7b3243b56e0b01240ed5a0f8cd4e823354dc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353268"
---
# <a name="idebugprimitivetypefieldgetprimitivetype"></a>IDebugPrimitiveTypeField::GetPrimitiveType
检索与此字段关联的基元类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPrimitiveType (
   DWORD* pdwType
);
```

```csharp
int GetPrimitiveType (
   out uint pdwType
);
```

## <a name="parameters"></a>参数
`pdwType`\
[out]值从[CorElementType 枚举](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)表示基元类型。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`。

## <a name="see-also"></a>请参阅
- [IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)