---
title: IDebug容器字段：：枚举场 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733227"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
为容器的字段创建枚举器。

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
[在]选择要枚举的字段[的FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)常量的组合。 字段类型可以描述存储类型，如类或基元，或特定信息，如本地、参数或"此"指针。

`dwModifiersFilter`\
[在]选择要枚举的字段的[FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)常量的组合。 字段修改器可以是访问权限（如公共或私有）或存储信息（如虚拟、静态或最终）。

`pszNameFilter`\
[在]要枚举的字段的名称。 如果要返回所有字段，这可以为空值。

`nameMatch`\
[在][NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)枚举中的值，用于控制搜索是否区分大小写。

`ppEnum`\
[出]返回表示字段列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象。 如果没有字段，则返回空值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或S_FALSE如果没有字段。 否则，返回错误代码。

## <a name="remarks"></a>备注
 可以`dwKindFilter`组合`dwModifiersFilter`和`pszNameFilter`参数，例如，选择名为"MyMethod"的所有公共虚拟方法。

## <a name="see-also"></a>请参阅
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
