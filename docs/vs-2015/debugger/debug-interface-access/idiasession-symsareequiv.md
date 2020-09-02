---
title: IDiaSession::symsAreEquiv | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ba8c77d7d97da75ce82fcbe732db64acf633b8af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150214"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检查两个符号是否等效。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT symsAreEquiv (   
   IDiaSymbol* symbolA,  
   IDiaSymbol* symbolB  
);  
```  
  
#### <a name="parameters"></a>参数  
 `symbolA`  
 中在比较中使用的第一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。  
  
 `symbolB`  
 中比较中使用的第二个 `IDiaSymbol` 对象。  
  
## <a name="return-value"></a>返回值  
 如果符号等效， `S_OK` 则返回; 否则返回 `S_FALSE` ，则符号不等效。 否则，将返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
