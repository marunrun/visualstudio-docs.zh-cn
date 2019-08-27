---
title: IDebugEnumField::GetStringFromValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cd7466e5390cff747532dca0343680cf359db46a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345089"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
此方法获取给定其值的枚举常量的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetStringFromValue(
   ULONGLONG value,
   BSTR*     pbstrValue
);
```

```csharp
int GetStringFromValue(
   ulong      value,
   out string pbstrValue
);
```

## <a name="parameters"></a>参数
`value`\
[in]要为其获取枚举的名称的常量值。

`pbstrValue`\
[out]返回的枚举常量的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果的值没有关联的名称，或返回错误代码。

## <a name="remarks"></a>备注
 如果有多个相同的值与关联的名称，将返回在枚举中定义的第一个名称。

## <a name="see-also"></a>请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)