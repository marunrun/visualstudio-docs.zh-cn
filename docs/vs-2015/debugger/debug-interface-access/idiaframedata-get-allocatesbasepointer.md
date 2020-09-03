---
title: IDiaFrameData::get_allocatesBasePointer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_allocatesBasePointer method
ms.assetid: 8a33db5d-008c-4fe5-b64f-210c9b77f686
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 90a32930c51caad61e07b0e6fdfe5b164a5515bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203671"
---
# <a name="idiaframedataget_allocatesbasepointer"></a>IDiaFrameData::get_allocatesBasePointer
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指示是否为此地址范围内的代码分配基指针。 不推荐使用此方法。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_allocatesBasePointer (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄 `TRUE` 如果分配基指针，则返回; 否则返回 `FALSE` 。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此属性应仅由以前访问 FPO_DATA 的代码使用，或在 [IDiaFrameData：： get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) 方法返回的程序字符串为时使用 `NULL` 。 否则，程序字符串将包含计算以前寄存器值所需的所有信息。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
