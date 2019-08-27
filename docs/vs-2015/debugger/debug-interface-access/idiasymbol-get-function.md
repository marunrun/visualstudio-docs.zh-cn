---
title: 'Idiasymbol:: Get_function |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_function method
ms.assetid: 48b3a318-3211-410f-8570-c02ee210f0a5
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e5248f94fed23a894fb1c7e988043f44bb27b7a4
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64784781"
---
# <a name="idiasymbolgetfunction"></a>IDiaSymbol::get_function
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指定公共符号是否引用的函数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_function (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回`TRUE`如果符号引用的函数; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="requirements"></a>要求  
  
|需求|描述|  
|-----------------|-----------------|  
|标头：|dia2.h|  
|版本：|DIA SDK v7.0|  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
