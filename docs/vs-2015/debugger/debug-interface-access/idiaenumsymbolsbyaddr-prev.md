---
title: IDiaEnumSymbolsByAddr::Prev | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Prev method
ms.assetid: da3b3dca-68cb-4cb0-b25c-e28a1ffe49d3
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f7a5debb0ffccffed4077c367d5b008a2a2a7cc2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189639"
---
# <a name="idiaenumsymbolsbyaddrprev"></a>IDiaEnumSymbolsByAddr::Prev
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

按地址检索前面的符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Prev (   
   ULONG        celt,   
   IDiaSymbol** rgelt,  
   ULONG*       pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 celt  
 中要检索的枚举器中的符号数。  
  
 rgelt  
 弄要用 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象填充的数组，这些对象表示所需的符号。  
  
 pceltFetched  
 弄返回提取的枚举器中的符号数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果没有前面的符号，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法按提取的元素数更新枚举器的位置。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
