---
title: 'Idiasymbol:: Get_isaggregated |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isAggregated method
ms.assetid: 24d280ef-6ea3-4958-9418-4ad3ca7c67c1
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9345aee08dcc5c27bfa6c20f9b5821d1875a5b99
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64822165"
---
# <a name="idiasymbolgetisaggregated"></a>IDiaSymbol::get_isAggregated
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，指定数据符号是否为聚合或集合的符号; 的一部分编译器会将聚合的符号视为单独的实体，但它们实际上是单个更大符号的一部分。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_isAggregated(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pFlag`  
 [out]返回`TRUE`如果数据是从父符号; 拆分的符号的聚合的一部分，否则将返回`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="remarks"></a>备注  
 [Idiasymbol:: Get_issplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)方法是`TRUE`符号是父级的聚合的符号。  
  
## <a name="requirements"></a>要求  
  
|需求|描述|  
|-----------------|-----------------|  
|标头：|dia2.h|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)
