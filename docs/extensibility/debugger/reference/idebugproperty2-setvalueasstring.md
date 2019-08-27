---
title: IDebugProperty2::SetValueAsString |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 27b481165cf95a97d7674d52d8553426dfb6417c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314604"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
从给定字符串中设置属性的值。

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
[in]包含要设置的值的字符串。

`nRadix`\
[in]用于解释任何数字信息的基数。 这可以是 0，以尝试自动确定基数。

`dwTimeout`\
[in]指定以毫秒为单位，此方法返回前等待的最长时间。 使用`INFINITE`无限期等待。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 下表显示了其他可能的值。

|值|描述|
|-----------|-----------------|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|字符串可以转换为属性值，或无法设置属性值。|
|`E_SETVALUE_VALUE_IS_READONLY`|该属性是只读的。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)