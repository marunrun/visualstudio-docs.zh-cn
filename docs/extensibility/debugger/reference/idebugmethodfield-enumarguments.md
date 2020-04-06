---
title: IDebugMethodField：：枚举 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumArguments
helpviewer_keywords:
- IDebugMethodField::EnumArguments method
ms.assetid: 3ab55488-2437-4ff6-a9ae-78ea6d7b23a8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: adbb1ea4c9172a5f1cee877d04b81aed938bf7a5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727260"
---
# <a name="idebugmethodfieldenumarguments"></a>IDebugMethodField::EnumArguments
为调用方法所需的每个参数的类型创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumArguments( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumArguments(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>参数
`ppParams`\
[出]返回表示参数类型列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象。 如果没有参数，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或返回S_FALSE如果没有参数。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是表示每个参数类型的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。 调用[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法以检索有关每个参数类型的信息。

 如果需要参数的名称和类型，则调用[Enum 参数](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)
