---
title: 'Idiaenumframedata:: Skip |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Skip method
ms.assetid: 67140b4c-7125-4895-932d-42412326da29
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ff8b58f6d36e9ce9759e2672f7e438bc0019fc1e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179493"
---
# <a name="idiaenumframedataskip"></a>IDiaEnumFrameData::Skip
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

跳过枚举序列中的帧数据元素的指定的数目。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Skip (   
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>参数  
 celt  
 [in]若要跳过枚举序列中的帧数据元素数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果没有更多记录要跳过。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
