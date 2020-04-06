---
title: IDebugenumfield：从Stringcase敏感获取价值 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 551945ded9d1ba3e973f18c21463a896cbd478c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730254"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
此方法使用不区分大小写的搜索来返回与枚举常量的名称关联的值。

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
[在]指定要为其获取值的名称的字符串。 请注意，对于C++，这是一个宽字符字符串。

`pValue`\
[出]返回关联的数值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，如果`S_FALSE`名称不是枚举的一部分，则返回 或错误代码。

## <a name="remarks"></a>备注
 此方法不区分大小写。 如果需要区分大小写搜索（例如，在名称区分大小写的C++）C++），请使用[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)。

## <a name="see-also"></a>请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)
