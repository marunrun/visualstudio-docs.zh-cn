---
title: 'Idiasymbol:: Get_thisadjust |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thisAdjust method
ms.assetid: 56b9a147-e8c0-4d4b-a42a-398214dd5f86
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 979f79658834f9bdcf50f0af51597515eaab2991
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64814070"
---
# <a name="idiasymbolgetthisadjust"></a>IDiaSymbol::get_thisAdjust
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索逻辑`this`精算师方法。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_thisAdjust (   
   LONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回逻辑`this`精算师方法。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="remarks"></a>备注  
 在某些多个继承情况下该方法本身必须计算真正`this`通过将添加到的偏移量值`this`。  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
