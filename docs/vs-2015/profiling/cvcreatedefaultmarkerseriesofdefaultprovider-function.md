---
title: CvCreateDefaultMarkerSeriesOfDefaultProvider 函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- cvmarkers/CvCreateDefaultMarkerSeriesOfDefaultProvider
helpviewer_keywords:
- CvCreateDefaultMarkerSeriesOfDefaultProvider method
ms.assetid: 24eb80f8-8fca-4c47-93b5-bb1eb8ffdffd
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fb0ab16dcd7e42a496317f4e7589bafdbdaf83dc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161996"
---
# <a name="cvcreatedefaultmarkerseriesofdefaultprovider-function"></a>CvCreateDefaultMarkerSeriesOfDefaultProvider 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建默认提供程序的默认标记系列。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CvCreateDefaultMarkerSeriesOfDefaultProvider(  
   _Out_ PCV_PROVIDER* ppProvider,  
   _Out_ PCV_MARKERSERIES* ppMarkerSeries  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppProvider`  
 提供程序对象变量的地址。 地址不能为 NULL，该变量可以具有任何值。  
  
 `ppMarkerSeries`  
 标记系列对象变量的地址。 地址不能为 NULL，该变量可以具有任何值。  
  
## <a name="return-value"></a>返回值  
 成功创建提供程序和标记系列时返回 S_OK，出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。  
  
## <a name="requirements"></a>要求  
 **标头：** cvmarkers.h  
  
## <a name="see-also"></a>另请参阅  
 [C++ 库参考](../profiling/cpp-library-reference.md)
