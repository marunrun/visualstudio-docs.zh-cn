---
title: CvReleaseMarkerSeries 函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseMarkerSeries
helpviewer_keywords:
- CvReleaseMarkerSeries method
ms.assetid: 3b4711ee-e534-411d-9128-f69cd7932a48
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6bfa9952a834110ef0fea36568ea210b637547aa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68177752"
---
# <a name="cvreleasemarkerseries-function"></a>CvReleaseMarkerSeries 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

发布标记系列。 在发布之后请勿使用标记系列对象，否则应用程序可能会崩溃。 标记系列发布失败会导致内存泄漏。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CvReleaseMarkerSeries(  
   _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pMarkerSeries`  
 提供程序对象变量的地址。 地址不能为 NULL，该变量可以具有任何值。  
  
## <a name="return-value"></a>返回值  
 成功发布标记系列时返回 S_OK，出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。  
  
## <a name="requirements"></a>要求  
 **标头：** cvmarkers.h  
  
## <a name="see-also"></a>另请参阅  
 [C++ 库参考](../profiling/cpp-library-reference.md)
