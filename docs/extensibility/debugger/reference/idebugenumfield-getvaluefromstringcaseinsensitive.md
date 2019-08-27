---
title: IDebugEnumField::GetValueFromStringCaseInsensitive |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72e6f79616c8c8099b938a29bc1d1809adb152a3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350069"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
此方法使用不区分大小写的搜索返回与枚举常量的名称相关联的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetValueFromStringCaseInsensitive(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromStringCaseInsensitive(
   string    pszValue,
   out ulong pValue
);
```

## <a name="parameters"></a>参数
`pszValue`\
[in]指定要为其获取值的名称的字符串。 请注意，对于C++，这是一个宽字符字符串。

`pValue`\
[out]返回关联的数字值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`，如果名称不是枚举或错误代码的一部分。

## <a name="remarks"></a>备注
 此方法是不区分大小写。 如果需要搜索区分大小写 (例如，在一种语言如C++名称是区分大小写)，使用[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)。

## <a name="see-also"></a>请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)