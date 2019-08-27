---
title: IDebugPropertyField::GetPropertySetter |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField::GetPropertySetter
helpviewer_keywords:
- IDebugPropertyField::GetPropertySetter method
ms.assetid: 744d76fd-2bcc-4917-a040-ce4cc714ef61
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29772ad76df6538ec5093d2fb34427a7fa89c5ff
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345683"
---
# <a name="idebugpropertyfieldgetpropertysetter"></a>IDebugPropertyField::GetPropertySetter
获取设置的属性的方法。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPropertySetter( 
   IDebugMethodField** ppField
);
```

```csharp
int GetPropertySetter(
   out IDebugMethodField ppField
);
```

## <a name="parameters"></a>参数
`ppField`\
[out]返回[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)表示的方法用于设置属性的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则将返回错误代码。

## <a name="remarks"></a>备注
 若要获取的属性的方法，调用[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)