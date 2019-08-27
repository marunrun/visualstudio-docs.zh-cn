---
title: IDiaEnumSymbolsByAddr::Next | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Next method
ms.assetid: a1320587-7ce7-401f-9548-2f8bcece5cc3
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fc58c8da54380b8a835d64fcc5dc079bb8d8023e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189648"
---
# <a name="idiaenumsymbolsbyaddrnext"></a>IDiaEnumSymbolsByAddr::Next
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索地址按顺序的下一个符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Next (   
   ULONG        celt,   
   IDiaSymbol** rgelt,  
   ULONG*       pceltFetched  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 celt  
 [in]要检索的枚举器中的符号数。  
  
 rgelt  
 [out]数组，它是在用来填充[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示所需的符号。  
  
 pceltFetched  
 [out]在提取枚举器返回的符号的数量。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多的符号。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法更新枚举器位置提取的元素数。  
  
## <a name="see-also"></a>请参阅  
 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
