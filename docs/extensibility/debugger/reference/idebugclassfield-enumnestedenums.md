---
title: IDebugClassField：：枚外数字 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedEnums
helpviewer_keywords:
- IDebugClassField::EnumNestedEnums method
ms.assetid: 90fd0cef-9145-4de6-91d4-6c881df39d6e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 38ee3ccd1ffd3130bc918da18c631cf08683f064
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734405"
---
# <a name="idebugclassfieldenumnestedenums"></a>IDebugClassField::EnumNestedEnums
为此类的嵌套枚举器创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumNestedEnums(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedEnums(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[出]返回表示嵌套枚举列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象。 如果没有嵌套枚举，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回S_OK或返回S_FALSE如果没有嵌套的枚举器。 否则，返回错误代码。

## <a name="remarks"></a>备注
枚举的每个元素都是描述嵌套枚举的[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)对象。

在类中声明的枚举被视为嵌套枚举。 例如，假定：

```
class RootClass {
    enum NestedEnum { EnumValue = 0 }
};
```

该方法`EnumNestedEnums`将返回一个[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，该对象包含一个表示枚举的`NestedEnum` [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)对象。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
