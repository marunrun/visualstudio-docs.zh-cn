---
title: IDebugGenericFieldDefinition::ConstructInstantiation | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ConstructInstantiation
- IDebugGenericFieldDefinition::ConstructInstantiation
ms.assetid: ef8ae261-a98b-4dc2-93b3-7c5191818ba2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89f7ecfc79cc2a4279a8ca0fccfc527ef63e603b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313210"
---
# <a name="idebuggenericfielddefinitionconstructinstantiation"></a>IDebugGenericFieldDefinition::ConstructInstantiation
构造给定类型的参数数组的字段实例。

## <a name="syntax"></a>语法

```cpp
HRESULT ConstructInstantiation(
   ULONG32       cArgs,
   IDebugField** ppArgs,
   IDebugField** ppConstructedField
);
```

```csharp
int ConstructInstantiation(
   uint            cArgs,
   IDebugField[]   ppArgs,
   out IDebugField ppConstructedField
);
```

## <a name="parameters"></a>参数
`cArgs`\
[in]中的参数数目`ppArgs`数组。

`ppArgs`\
[in]包含的类型参数的数组。 类型参数必须为封闭的类型 （非泛型或完全实例化泛型）。

`ppConstructedField`\
[out]返回[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口，表示新字段。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 不会检查约束。

## <a name="see-also"></a>请参阅
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)