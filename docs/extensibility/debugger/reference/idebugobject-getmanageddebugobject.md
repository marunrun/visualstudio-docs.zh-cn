---
title: IDebugObject：获取托管调试对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67d0d7a8642c9dd90067b0e197f420d4cc821faa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726689"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
在调试引擎的地址空间中创建托管对象的副本。

## <a name="syntax"></a>语法

```cpp
HRESULT GetManagedDebugObject( 
   IDebugManagedObject** ppObject
);
```

```csharp
int GetManagedDebugObject(
   out IDebugManagedObject ppObject
);
```

## <a name="parameters"></a>参数
`ppObject`\
[出]返回表示新创建的托管对象的[IDebug 托管对象](../../../extensibility/debugger/reference/idebugmanagedobject.md)。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。 如果此[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)不表示托管值类实例，则返回E_FAIL。

## <a name="remarks"></a>备注
 此[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)必须表示托管值类实例，如`System.Decimal`实例。 通过具有本地副本，可以消除调用[评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)的开销。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
