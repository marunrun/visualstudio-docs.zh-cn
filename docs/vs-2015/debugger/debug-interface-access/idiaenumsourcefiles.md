---
title: IDiaEnumSourceFiles | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles interface
ms.assetid: 5c0779a6-a2ea-408a-90da-ebdecf2b83c0
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8b095515be5e3c032667c96d8b13d92aa5995c7f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189726"
---
# <a name="idiaenumsourcefiles"></a>IDiaEnumSourceFiles
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数据源中包含的各种源文件。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaEnumSourceFiles : IUknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaEnumSourceFiles`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaEnumSourceFiles::get__NewEnum](../../debugger/debug-interface-access/idiaenumsourcefiles-get-newenum.md)|检索`IEnumVARIANT Interface`此枚举器的版本。|  
|[IDiaEnumSourceFiles::get_Count](../../debugger/debug-interface-access/idiaenumsourcefiles-get-count.md)|检索源文件的数目。|  
|[IDiaEnumSourceFiles::Item](../../debugger/debug-interface-access/idiaenumsourcefiles-item.md)|通过索引检索源文件。|  
|[IDiaEnumSourceFiles::Next](../../debugger/debug-interface-access/idiaenumsourcefiles-next.md)|检索指定的数目的枚举序列中的源文件。|  
|[IDiaEnumSourceFiles::Skip](../../debugger/debug-interface-access/idiaenumsourcefiles-skip.md)|跳过枚举序列中的源文件指定的数目。|  
|[IDiaEnumSourceFiles::Reset](../../debugger/debug-interface-access/idiaenumsourcefiles-reset.md)|将枚举序列重置到开头。|  
|[IDiaEnumSourceFiles::Clone](../../debugger/debug-interface-access/idiaenumsourcefiles-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方的说明  
 通过调用来获取此接口`QueryInterface`方法[IDiaTable](../../debugger/debug-interface-access/idiatable.md)对象。 请参阅详细信息的示例。  
  
## <a name="example"></a>示例  
 此示例演示如何获取`IDiaEnumSourceFiles`DIA 会话对象中的表列表中的接口。 有关访问源文件信息的示例，请参阅[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)接口。  
  
```cpp#  
  
IDiaEnumSourceFiles* GetEnumSourceFiless(IDiaSession *pSession)  
{  
    IDiaEnumSourceFiles * pUnknown    = NULL;  
    REFIID                iid         = __uuidof(IDiaEnumSourceFiles);  
    IDiaEnumTables*       pEnumTables = NULL;  
    IDiaTable*            pTable      = NULL;  
    ULONG                 celt        = 0;  
  
    if (pSession->getEnumTables(&pEnumTables) != S_OK)  
    {  
        wprintf(L"ERROR - GetTable() getEnumTables\n");  
        return NULL;  
    }  
    while (pEnumTables->Next(1, &pTable, &celt) == S_OK && celt == 1)  
    {  
        // There is only one table that matches the given iid  
        HRESULT hr = pTable->QueryInterface(iid, (void**)&pUnknown);  
        pTable->Release();  
        if (hr == S_OK)  
        {  
            break;  
        }  
    }  
    pEnumTables->Release();  
    return pUnknown;  
}  
```  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)   
 [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)   
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
