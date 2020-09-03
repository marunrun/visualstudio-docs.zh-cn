---
title: IDebugContainerField：： EnumFields |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afc461d52f81afc2c2e7127a90313bea7b9dacf3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80733227"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
创建容器字段的枚举器。

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
中选择要枚举的字段 [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 常量的组合。 字段类型可以描述存储类型，如类或基元，或特定的信息，例如本地、参数或 "this" 指针。

`dwModifiersFilter`\
中选择要枚举的字段 [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md) 常量的组合。 字段修饰符可以是访问权限（如公共或私有）或存储信息（如虚拟、静态或最终）。

`pszNameFilter`\
中要枚举的字段的名称。 如果要返回所有字段，则此值可以为 null 值。

`nameMatch`\
中 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) 枚举中的一个值，该值控制搜索是否区分大小写。

`ppEnum`\
弄返回表示字段列表的 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有字段，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或 S_FALSE （如果没有任何字段）。 否则，返回错误代码。

## <a name="remarks"></a>备注
 `dwKindFilter`例如， `dwModifiersFilter` `pszNameFilter` 可以组合、和参数，以选择名为 "MyMethod" 的所有公共虚拟方法。

## <a name="see-also"></a>另请参阅
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
