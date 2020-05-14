---
title: IDebugMethodfield：：EnumStaticLocals |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumStaticLocals
helpviewer_keywords:
- IDebugMethodField::EnumStaticLocals method
ms.assetid: e0c522c4-f759-4c32-ae87-7abcb573e77d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e0a89b4c1ac4318b6dd070dc086b86b45ad24fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727151"
---
# <a name="idebugmethodfieldenumstaticlocals"></a>IDebugMethodField::EnumStaticLocals
为方法的静态局部变量创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumStaticLocals( 
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumStaticLocals(
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>参数
`ppLocals`\
[出]返回表示静态局部变量列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象。 如果没有静态局部变量，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或返回S_FALSE如果没有静态局部变量。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是一个[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象，表示不同类型的静态局部变量。 调用每个对象上的[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法，以确定对象表示的静态局部类型。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
