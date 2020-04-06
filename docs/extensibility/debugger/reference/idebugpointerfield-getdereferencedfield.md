---
title: IDebugPointer字段：获取被引用字段 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 617711a611e6eb1ea162c3abd8ad2b793b4756cb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725620"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
此方法返回此指针对象指向的对象类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDereferencedField(
   IDebugField** ppField
);
```

```csharp
int GetDereferencedField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`ppField`\
[出]返回描述目标对象类型的[IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 例如，如果[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)对象指向整数，则此方法返回的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)类型将描述该整数类型。

## <a name="see-also"></a>请参阅
- [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
