---
title: IDebugContainerField::EnumFields |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6d3edeb677af728b1a0fd0e9cf8685e7919d79e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317932"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
创建容器的字段的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumFields( 
   FIELD_KIND         dwKindFilter,
   FIELD_MODIFIERS    dwModifiersFilter,
   LPCOLESTR          pszNameFilter,
   NAME_MATCH         nameMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumFields(
   enum_ FIELD_KIND      dwKindFilter,
   enum_ FIELD_MODIFIERS dwModifiersFilter,
   string                pszNameFilter,
   NAME_MATCH            nameMatch,
   out IEnumDebugFields  ppEnum
);
```

## <a name="parameters"></a>参数
`dwKindFilter`\
[in]组合[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)选择要枚举的字段的常量。 字段类型可以描述存储类型，如类或基元，或特定的信息，如本地、 参数或"this"指针。

`dwModifiersFilter`\
[in]组合[FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)选择要枚举的字段的常量。 字段修饰符可以是访问权限，如公共或私有或存储信息，如虚拟、 静态的或最后一个。

`pszNameFilter`\
[in]要枚举的字段的名称。 如果要返回所有字段，这可以是 null 值。

`nameMatch`\
[in]中的值[NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)枚举，用于控制是否搜索是否区分大小写。

`ppEnum`\
[out]返回[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，表示的字段的列表。 如果没有字段，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，返回 S_OK 或 S_FALSE 如果没有字段。 否则，返回错误代码。

## <a name="remarks"></a>备注
 `dwKindFilter`， `dwModifiersFilter`，和`pszNameFilter`参数可以结合使用，例如，若要选择名为"MyMethod"的所有公共虚拟方法。

## <a name="see-also"></a>请参阅
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)