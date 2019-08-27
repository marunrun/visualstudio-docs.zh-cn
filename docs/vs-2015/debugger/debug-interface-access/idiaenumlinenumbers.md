---
title: IDiaEnumLineNumbers | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers interface
ms.assetid: cdf07b4f-19e4-4dcd-8af8-c2dbca586a7c
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 87d5450cddab6b3cd230040175d18ae186483b30
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687201"
---
# <a name="idiaenumlinenumbers"></a>IDiaEnumLineNumbers
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数据源中包含的各种行号。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaEnumLineNumbers : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaEnumLineNumbers`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaEnumLineNumbers::get__NewEnum](../../debugger/debug-interface-access/idiaenumlinenumbers-get-newenum.md)|检索[IEnumVARIANT 接口](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e)此枚举器的版本。|  
|[IDiaEnumLineNumbers::get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md)|检索数目的行号。|  
|[IDiaEnumLineNumbers::Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)|通过索引中检索行号。|  
|[IDiaEnumLineNumbers::Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md)|检索指定的数目的枚举序列中的行号。|  
|[IDiaEnumLineNumbers::Skip](../../debugger/debug-interface-access/idiaenumlinenumbers-skip.md)|将跳过指定的数目的枚举序列中的行号。|  
|[IDiaEnumLineNumbers::Reset](../../debugger/debug-interface-access/idiaenumlinenumbers-reset.md)|将枚举序列重置到开头。|  
|[IDiaEnumLineNumbers::Clone](../../debugger/debug-interface-access/idiaenumlinenumbers-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口通过调用中的以下方法之一获取[IDiaSession](../../debugger/debug-interface-access/idiasession.md)接口：  
  
- [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)  
  
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)  
  
- [IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)  
  
- [IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)  
  
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)  
  
## <a name="example"></a>示例  
 此示例演示如何获取`IDiaEnumLineNumbers`从会话的接口。 在这种情况下，该示例演示如何获取函数的行号枚举 (由`pSymbol`)。 使用行号的更完整示例，请参阅[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)接口。  
  
```cpp#  
void dumpFunctionLines( IDiaSymbol* pSymbol, IDiaSession* pSession )  
{  
    ULONGLONG length = 0;  
    DWORD isect = 0;  
    DWORD offset = 0;  
    pSymbol->get_addressSection( &isect );  
    pSymbol->get_addressOffset( &offset );  
    pSymbol->get_length( &length );  
    if ( isect != 0 && length > 0 )  
    {  
        CComPtr< IDiaEnumLineNumbers > pLines;  
        if ( SUCCEEDED( pSession->findLinesByAddr(  
                                      isect,  
                                      offset,  
                                      static_cast<DWORD>( length ),  
                                      &pLines )  
                      )  
           )  
        {  
            // Do something with the enumeration  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)   
 [IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)   
 [IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)   
 [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)   
 [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)
