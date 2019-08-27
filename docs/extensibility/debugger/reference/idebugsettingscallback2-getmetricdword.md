---
title: IDebugSettingsCallback2::GetMetricDword | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricDword
ms.assetid: 831a5a1a-c4af-4520-9fdf-3a731aeff85c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc685d043b405fbd78a446722e41df4ca584b8e3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322037"
---
# <a name="idebugsettingscallback2getmetricdword"></a>IDebugSettingsCallback2::GetMetricDword
检索在给定名称的指标的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMetricDword(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   DWORD*  pdwValue
);
```

```csharp
private int GetMetricDword(
   string   pszType,
   ref Guid guidSection,
   string   pszMetric,
   out uint pdwValue
);
```

## <a name="parameters"></a>参数
`pszType`\
[in]该度量值的类型。

`guidSection`\
[in]部分中的唯一标识符。

`pszMetric`\
[in]指标的名称。

`pdwValue`\
[out]返回的指标值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)