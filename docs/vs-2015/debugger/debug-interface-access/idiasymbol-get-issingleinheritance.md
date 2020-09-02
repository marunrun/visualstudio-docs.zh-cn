---
title: IDiaSymbol：： get_isSingleInheritance |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 46cde656-059b-4c20-9476-3ca68ccc9912
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 70b99b852175febe448e7b821070261d6abda4b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151456"
---
# <a name="idiasymbolget_issingleinheritance"></a>IDiaSymbol::get_isSingleInheritance
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定指针是否 `this` 指向具有单一继承的数据成员。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT get_isSingleInheritance(   
   BOOL* pRetVal);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄指向 `BOOL` 的指针，该指针指定 `this` 指针是否指向具有单一继承的数据成员。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
