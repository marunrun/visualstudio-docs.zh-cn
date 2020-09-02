---
title: BasicType | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- BasicType enumeration
ms.assetid: 19ae53ba-cd6e-47b6-9f94-27ae663ce955
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 38de89b9774ac20f67b91e4ba864534122f4cdb0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580832"
---
# <a name="basictype"></a>BasicType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定符号的基本类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum BasicType {   
   btNoType   = 0,  
   btVoid     = 1,  
   btChar     = 2,  
   btWChar    = 3,  
   btInt      = 6,  
   btUInt     = 7,  
   btFloat    = 8,  
   btBCD      = 9,  
   btBool     = 10,  
   btLong     = 13,  
   btULong    = 14,  
   btCurrency = 25,  
   btDate     = 26,  
   btVariant  = 27,  
   btComplex  = 28,  
   btBit      = 29,  
   btBSTR     = 30,  
   btHresult  = 31  
};  
```  
  
## <a name="elements"></a>元素  
 btNoType  
 未指定基本类型。  
  
 btVoid  
 基本类型是 `void` 。  
  
 btChar  
 基本类型为 `char`)  (c/c + + 类型。  
  
 btWChar  
 基本类型是 (Unicode) 字符 (`WCHAR`) 。  
  
 btInt  
 基本类型为 `signed int`)  (c/c + + 类型。  
  
 btUInt  
 基本类型为 `unsigned int`)  (c/c + + 类型。  
  
 btFloat  
 基本类型是 () 的浮点数 `FLOAT` 。  
  
 btBCD  
 基本类型是二进制编码的十进制 (`BCD`) 。  
  
 btBool  
 基本类型是布尔 (`BOOL`) 。  
  
 btLong  
 基本类型为 `long int`)  (c/c + + 类型。  
  
 btULong  
 基本类型为 `unsigned long int`)  (c/c + + 类型。  
  
 btCurrency  
 基本类型为 currency。  
  
 btDate  
 基本类型是日期/时间 (`DATE`) 。  
  
 btVariant  
 基本类型是 () 的变量类型结构 `VARIANT` 。  
  
 btComplex  
 基本类型为复数。  
  
 btBit  
 基本类型是一位。  
  
 btBSTR  
 基本类型是基本或二进制字符串 (`BSTR`) 。  
  
 btHresult  
 基本类型是 `HRESULT` 。  
  
## <a name="remarks"></a>备注  
 此枚举中的值由 [IDiaSymbol：： get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md) 方法返回。  
  
## <a name="requirements"></a>要求  
 标头： cvconst  
  
## <a name="see-also"></a>另请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol：： get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)   
 [IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)
