---
title: IDebugClassField::EnumNestedClasses |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedClasses
helpviewer_keywords:
- IDebugClassField::EnumNestedClasses method
ms.assetid: 2ba5ef0c-395e-4006-9e3c-9b06e1d711d0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75b963f7a342a9ce2b276cc03ea5dece9316ff6d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313125"
---
# <a name="idebugclassfieldenumnestedclasses"></a>IDebugClassField::EnumNestedClasses
创建此类中嵌套的类的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumNestedClasses(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedClasses(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]返回[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，表示的嵌套类的列表。 如果不有任何嵌套的类，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回 S_OK 或如果没有嵌套的类，则返回 S_FALSE。 否则，返回错误代码。

## <a name="remarks"></a>备注
枚举每个元素均[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)描述嵌套的类的对象。

嵌套的类是在另一个类中定义的类。 例如：

```
class RootClass {
   class NestedClass { }
};
```

[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)枚举将包含一个对象，表示`NestedClass`类。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
