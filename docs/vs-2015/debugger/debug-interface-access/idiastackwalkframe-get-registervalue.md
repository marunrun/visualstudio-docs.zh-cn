---
title: IDiaStackWalkFrame::get_registerValue | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::get_registerValue method
ms.assetid: ca3c20a9-934a-4b2c-a7f6-7d06e8611ff2
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8c420266d08550398f33c2e2da9ba1b7bc41b5dc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68141919"
---
# <a name="idiastackwalkframegetregistervalue"></a>IDiaStackWalkFrame::get_registerValue
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索寄存器的值。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_registerValue (   
   DWORD      index,  
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `index`  
 [in]中的值[CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)指定注册以获取其值的枚举。  
  
 `pRetVal`  
 [out]返回注册的当前值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)   
 [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)
