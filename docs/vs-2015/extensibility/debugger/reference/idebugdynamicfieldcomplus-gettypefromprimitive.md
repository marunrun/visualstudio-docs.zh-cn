---
title: IDebugDynamicFieldCOMPlus::GetTypeFromPrimitive | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus::GetTypeFromPrimitive
- GetTypeFromPrimitive
ms.assetid: d7f51e2a-1b72-489c-b7b6-4af7b7e4d663
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd843f488439370ad652b52949b524e0ecca8af8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198472"
---
# <a name="idebugdynamicfieldcomplusgettypefromprimitive"></a>IDebugDynamicFieldCOMPlus::GetTypeFromPrimitive
检索给定其基元类型的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeFromPrimitive(
   DWORD         dwCorElementType,
   IDebugField** ppType
);
```

```csharp
int GetTypeFromPrimitive(
   uint            dwCorElementType,
   out IDebugField ppType
);
```

#### <a name="parameters"></a>参数
 `dwCorElementType`

 [in]值从[CorElementType 枚举](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)表示基元类型。

 `ppType`

 [out]返回[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)表示的类型。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)