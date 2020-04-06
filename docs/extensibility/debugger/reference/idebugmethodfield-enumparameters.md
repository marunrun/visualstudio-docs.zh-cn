---
title: IDebugMethodField：枚举参数 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumParameters
helpviewer_keywords:
- IDebugMethodField::EnumParameters method
ms.assetid: d77b1197-deb6-4144-8d1b-8b09949ccfac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13df02cf5870e630c4aecb34e9295d218ba7a0eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727199"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
为方法的参数创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumParameters( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumParameters(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>参数
`ppParams`\
[出]返回表示方法参数列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象;否则，如果没有参数，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或返回S_FALSE如果没有参数。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是表示不同类型的参数的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。 调用每个对象上的[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法，以确定对象表示的参数类型。

 参数包括其变量名称和类型。 类方法的第一个参数通常是"this"指针。

 如果只需要参数的类型，请调用[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)
