---
title: IDiaSymbol::get_typeIds | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 410f8afdac24139791c19c3936049c855a51d4f9
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "91146900"
---
# <a name="idiasymbolget_typeids"></a>IDiaSymbol::get_typeIds
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索此符号的编译器特定类型标识符值的数组。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_typeIds (   
   DWORD  cTypeIds,  
   DWORD* pcTypeIds,  
   DWORD  typeIds[]  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cTypeIds`  
 中用于保存数据的缓冲区大小。  
  
 `pcTypeIds`  
 弄返回 `typeIds` 已写入的数量，如果 `typeIds` 为 `NULL` ，则返回可用的类型标识符的总数。  
  
 `typeIds[]`  
 弄要使用类型标识符填充的数组。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
