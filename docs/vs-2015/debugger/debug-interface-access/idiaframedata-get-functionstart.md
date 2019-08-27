---
title: IDiaFrameData::get_functionStart | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_functionStart method
ms.assetid: 49fd24fb-65c2-4812-8303-56a968353e1b
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 08029b3abc3ec054cd8244d22d17db7992fa3623
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186937"
---
# <a name="idiaframedatagetfunctionstart"></a>IDiaFrameData::get_functionStart
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指示块是否包含一个函数的入口点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_functionStart (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pRetVal`  
 [out]返回`TRUE`如果块包含入口点; 否则返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 很可能不是函数的开始，因为帧代表或插入到一个函数的函数的内联方法的堆栈帧。  
  
## <a name="see-also"></a>请参阅  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
