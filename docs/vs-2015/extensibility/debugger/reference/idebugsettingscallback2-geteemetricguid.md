---
title: IDebugSettingsCallback2::GetEEMetricGuid |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEEMetricGuid
ms.assetid: 3d70c19a-595d-44f1-a7b3-a0cf8f15e371
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1cf70c424856b93eb4d082a167bc671b885a346
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155192"
---
# <a name="idebugsettingscallback2geteemetricguid"></a>IDebugSettingsCallback2::GetEEMetricGuid
检索在给定其名称的表达式计算器指标的唯一标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEEMetricGuid(
   REFGUID guidLang,
   REFGUID guidVendor,
   LPCWSTR pszMetric,
   GUID*   pguidValue
);
```

```csharp
HRESULT GetEEMetricGuid(
   ref Guid guidLang,
   ref Guid guidVendor,
   string   pszMetric,
   out Guid pguidValue
);
```

#### <a name="parameters"></a>参数
 `guidLang`

 [in]编程语言的唯一标识符。

 `guidVendor`

 [in]供应商的唯一标识符。

 `pszMetric`

 [in]指标的名称。

 `pguidValue`

 [out]返回度量值的唯一标识符。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)