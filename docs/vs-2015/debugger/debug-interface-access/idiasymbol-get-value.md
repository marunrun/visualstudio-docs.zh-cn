---
title: IDiaSymbol::get_value | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_value method
ms.assetid: 2e40174a-2a61-4e5f-bb32-9e0ceec2178a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e9000a4d0a65fd450e3ef655e6b646990f682ba9
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64837924"
---
# <a name="idiasymbolgetvalue"></a>IDiaSymbol::get_value
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个常量值。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_value (   
   VARIANT* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 [in、 out]一个`VARIANT`使用的常量的值填充的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。  
  
> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。  
  
## <a name="remarks"></a>备注  
 传递给此方法之前，必须初始化的提供的变体。 有关详细信息，请参阅示例。  
  
## <a name="example"></a>示例  
  
```cpp#  
void ProcessValue(IDiaSymbol *pSymbol)  
{  
    VARIANT value;  
    value.vt = VT_EMPTY;    // Initialize variant for use.  
    if (pSymbol->get_value(&value) == S_OK)  
    {  
        // Do something with value.  
    }  
}  
  
//----------------------------------------------------  
// Alternate approach  
void ProcessValue2(IDiaSymbol *pSymbol)  
{  
    CComVariant value;  
    if (pSymbol->get_value(&value) == S_OK)  
    {  
        // Do something with value  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
