---
title: IDebugSettingsCallback2::GetEELocalObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEELocalObject
ms.assetid: e69a3469-a049-420c-b918-c48a1e7b9baf
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e6bf186d8b4bf660cc4a22e962754e859378674
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202480"
---
# <a name="idebugsettingscallback2geteelocalobject"></a>IDebugSettingsCallback2::GetEELocalObject
检索给定的指标名称的表达式计算器本地对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEELocalObject(
   REFGUID     guidLang,
   REFGUID     guidVendor,
   LPCWSTR     pszMetric,
   IUnknown ** ppUnk
);
```

```csharp
private int GetEELocalObject(
   ref Guid          guidLang,
   ref Guid          guidVendor,
   string            pszMetric,
   out System.Object ppUnk
);
```

#### <a name="parameters"></a>参数
 `guidLang`

 [in]编程语言的唯一标识符。

 `guidVendor`

 [in]供应商的唯一标识符。

 `pszMetric`

 [in]指标的名称。

 `ppUnk`

 [out]返回的表达式计算器本地对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)