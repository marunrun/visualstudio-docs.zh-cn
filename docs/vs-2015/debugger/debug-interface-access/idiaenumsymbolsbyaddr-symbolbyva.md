---
title: IDiaEnumSymbolsByAddr::symbolByVA | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::symbolByVA method
ms.assetid: ac84339f-70c6-48ed-85d0-6d7d1b5194e8
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 325bbecf3a34a00664a9f63cdbf995bd14138d7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194883"
---
# <a name="idiaenumsymbolsbyaddrsymbolbyva"></a>IDiaEnumSymbolsByAddr::symbolByVA
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数定位通过按虚拟地址 (VA) 执行查找。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT symbolByVA (   
   DWORD**      virtualAddress,  
   IDiaSymbol** ppsymbol  
);  
```  
  
#### <a name="parameters"></a>参数  
 virtualAddress  
 [in]虚拟地址。  
  
 ppsymbol  
 [out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示找到的符号。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果找不到符号。 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
