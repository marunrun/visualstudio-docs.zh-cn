---
title: IDebugSettings 回拨2：：获取MetricDword |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricDword
ms.assetid: 831a5a1a-c4af-4520-9fdf-3a731aeff85c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3b8890cb76d8f15ff0519db5e20d3b8e8866d4eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720023"
---
# <a name="idebugsettingscallback2getmetricdword"></a>IDebugSettingsCallback2::GetMetricDword
检索给定指标名称的指标的值。

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
[在]指标的类型。

`guidSection`\
[在]节的唯一标识符。

`pszMetric`\
[在]指标的名称。

`pdwValue`\
[出]返回指标的值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
