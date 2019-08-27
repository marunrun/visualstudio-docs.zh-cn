---
title: IDebugSettingsCallback2::GetMetricString | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricString
- GetMetricString
ms.assetid: ecc875a2-8ac6-444c-a839-5191a780fd6b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 119fa1ac0f90cd6ebef22633130a3683c039a204
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321977"
---
# <a name="idebugsettingscallback2getmetricstring"></a>IDebugSettingsCallback2::GetMetricString
检索在给定名称的度量值的值字符串。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMetricString(
    LPCWSTR pszType,
    REFGUID guidSection,
    LPCWSTR pszMetric,
    BSTR*   pbstrValue
);
```

```csharp
private int GetMetricString(
    string     pszType,
    ref Guid   guidSection,
    string     pszMetric,
    out string pbstrValue
);
```

## <a name="parameters"></a>参数
`pszType`\
[in]该度量值的类型。

`guidSection`\
[in]部分中的唯一标识符。

`pszMetric`\
[in]指标的名称。

`pbstrValue`\
[out]返回度量值的值字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)