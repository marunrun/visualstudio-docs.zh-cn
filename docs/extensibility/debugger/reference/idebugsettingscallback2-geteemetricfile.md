---
title: IDebugSettingsCallback2::GetEEMetricFile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEEMetricFile
ms.assetid: 3a0bf9e5-bbd2-4d15-840d-8244732787fc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 824b947af25ef825d4f02983e17ecad3105028f3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322145"
---
# <a name="idebugsettingscallback2geteemetricfile"></a>IDebugSettingsCallback2::GetEEMetricFile
检索给定的名称或该度量值的表达式计算器指标文件。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEEMetricFile(
   REFGUID guidLang,
   REFGUID guidVendor,
   LPCWSTR pszMetric,
   BSTR*   pbstrValue
);
```

```csharp
private int GetEEMetricFile(
   ref Guid   guidLang,
   ref Guid   guidVendor,
   string     pszMetric,
   out string pbstrValue
);
```

## <a name="parameters"></a>参数
`guidLang`\
[in]编程语言的唯一标识符。

`guidVendor`\
[in]供应商的唯一标识符。

`pszMetric`\
[in]指标的名称。

`pbstrValue`\
[out]以字符串形式返回度量值的文件的内容。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)