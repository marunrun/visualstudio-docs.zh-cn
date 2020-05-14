---
title: IDebug属性2：：设置价值字符串 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 112ded163f38b93e9918387d8ca6beafb8282647
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721237"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
设置给定字符串中属性的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValueAsString ( 
   LPCOLESTR pszValue,
   UINT      nRadix,
   DWORD     dwTimeout
);
```

```csharp
int SetValueAsString ( 
   string pszValue,
   uint   nRadix,
   uint   dwTimeout
);
```

## <a name="parameters"></a>参数
`pszValue`\
[在]包含要设置的值的字符串。

`nRadix`\
[在]用于解释任何数值信息的半径。 这可以是 0，以尝试自动确定半径。

`dwTimeout`\
[在]指定从此方法返回之前等待的最大时间（以毫秒为单位）。 用于`INFINITE`无限期等待。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则返回错误代码。 下表显示了其他可能的值。

|值|说明|
|-----------|-----------------|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法将字符串转换为属性值，或者无法设置属性值。|
|`E_SETVALUE_VALUE_IS_READONLY`|属性为只读属性。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
