---
title: 'Idiasymbol:: Get_nostackordering |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noStackOrdering method
ms.assetid: a1753917-705b-4165-9880-d05e91e6dcb4
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5e07bf52f86cbf55c46c82f685afd63327545dcd
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "65698230"
---
# <a name="idiasymbolgetnostackordering"></a>IDiaSymbol::get_noStackOrdering
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

此函数可检索一个标志，指示是否可以作为堆栈缓冲区检查的一部分实现没有堆栈排序 ([/GS （缓冲区安全检查）](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e)编译器选项)。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_noStackOrdering(  
   BOOL *pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [out]返回`TRUE`如果没有堆栈的排序方式可以实现一部分堆栈缓冲区检查; 否则，返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="requirements"></a>要求  
  
|需求|描述|  
|-----------------|-----------------|  
|标头：|dia2.h|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [/GS（缓冲区安全检查）](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e)
