---
title: IDiaSession::symbolById | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symbolById method
ms.assetid: 062e4b5a-9c4d-4703-88da-ec13102c2b66
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ac409edcee7657e724822d1a72737c3142d8d93e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150207"
---
# <a name="idiasessionsymbolbyid"></a>IDiaSession::symbolById
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索由其唯一标识符的符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT symbolById (   
   DWORD        id,  
   IDiaSymbol** ppSymbol  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `id`  
 [in]唯一标识符。  
  
 `ppSymbol`  
 [out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)检索表示该符号的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 指定的标识符是由 DIA SDK 在内部使用，以使所有符号是唯一的唯一值。  
  
 此方法可以使用，例如，若要检索表示类型的另一种符号的符号 （参阅示例）。  
  
## <a name="example"></a>示例  
 此示例检索[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)表示的另一种符号类型。 此示例演示如何使用`symbolById`会话中的方法。 更简单的方法是调用[idiasymbol:: Get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)方法直接检索类型符号。  
  
```cpp#  
IDiaSymbol *GetSymbolType(IDiaSymbol *pSymbol, IDiaSession *pSession)  
{  
    IDiaSymbol *pTypeSymbol = NULL;  
    if (pSymbol != NULL && pSession != NULL)  
    {  
        DWORD symbolTypeId;  
        pSymbol->get_typeId(&symbolTypeId);  
        pSession->symbolById(symbolTypeId, &pTypeSymbol);  
    }  
    return(pTypeSymbol);  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
