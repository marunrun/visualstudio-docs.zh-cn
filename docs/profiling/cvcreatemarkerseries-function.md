---
title: CvCreateMarkerSeries 函数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvCreateMarkerSeriesA
- cvmarkers/CvCreateMarkerSeriesW
helpviewer_keywords:
- CvCreateMarkerSeriesA method
- CvCreateMarkerSeriesW method
ms.assetid: e280530b-137a-43a7-8643-aa514ab86ed7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eb3ef4d928aaac57f39a48e5be212c1148ef58eb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552676"
---
# <a name="cvcreatemarkerseries-function"></a>CvCreateMarkerSeries 函数
为给定提供程序创建标记系列。

## <a name="syntax"></a>语法

```C
_Check_return_ HRESULT CvCreateMarkerSeriesW(
    _In_ PCV_PROVIDER  pProvider,
    _In_ LPCWSTR pSeriesName,
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);

_Check_return_ HRESULT CvCreateMarkerSeriesA(
    _In_ PCV_PROVIDER  pProvider,
    _In_ LPCSTR pSeriesName,
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);
```

#### <a name="parameters"></a>参数
 `pProvider` 先前由 CvInitProvider 初始化的提供程序对象。 不能为 NULL。

 `pSeriesName` 标记系列名称。 不能为 NULL，但允许空字符串。

 `ppMarkerSeries` 输出变量的地址，用于存储标记系列上下文。 不能为 NULL。

## <a name="return-value"></a>返回值
 成功创建标记系列时返回 S_OK，出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。

## <a name="requirements"></a>要求
 **标头：** cvmarkers.h

 **Unicode：** CvCreateMarkerSeriesW

 **ANSI：** CvCreateMarkerSeriesA

## <a name="see-also"></a>请参阅
- [C++ 库参考](../profiling/cpp-library-reference.md)