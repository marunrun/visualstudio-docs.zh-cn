---
title: IDiaFrameData::get_lengthBlock | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthBlock method
ms.assetid: 2e54deb7-7744-428e-913c-1d47a2aa89b0
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7d66e8cd69836a6c2f8ee1052f5f5f7ff789f736
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552535"
---
# <a name="idiaframedatagetlengthblock"></a>IDiaFrameData::get_lengthBlock
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索的长度，以字节为单位的所述的帧的代码块。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_lengthBlock (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]在帧中返回的代码的字节数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 中的计划字符串解释通常使用此方法返回的值 (请参阅[idiaframedata:: Get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)程序字符串的定义的方法)。  
  
## <a name="see-also"></a>请参阅  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
