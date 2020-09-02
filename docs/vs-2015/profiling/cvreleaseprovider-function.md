---
title: CvReleaseProvider 函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseProvider
helpviewer_keywords:
- CvReleaseProvider method
ms.assetid: 8d74379e-295d-452b-bd5f-0769df387d4f
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7d5e611c2a964fcbb78a387a09989436e672ecd6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551229"
---
# <a name="cvreleaseprovider-function"></a>CvReleaseProvider 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

发布标记提供程序。 发布标记提供程序不会影响此提供程序以前创建的标记系列。 标记系列必须由 CvReleaseMarkerSeries 调用单独发布。 提供程序发布失败会导致内存泄漏。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CvReleaseProvider(  
   _In_ PCV_PROVIDER pProvider  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pProvider`  
 提供程序上下文。 不能为 NULL。  
  
## <a name="return-value"></a>返回值  
 成功发布提供程序时返回 S_OK，出现任何错误时返回错误代码。 使用 SUCCEEDED/FAILED 宏检查错误条件。  
  
## <a name="requirements"></a>要求  
 **标头：** cvmarkers.h  
  
## <a name="see-also"></a>另请参阅  
 [C + + 库参考](../profiling/cpp-library-reference.md)
