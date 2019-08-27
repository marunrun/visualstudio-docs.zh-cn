---
title: IDiaEnumInjectedSources | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources interface
ms.assetid: f97e2392-22e1-48da-b7ce-ad94c8b684b0
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e710e586f3ece4fdf0cdbf9bee2bcc70f4ab87b5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687204"
---
# <a name="idiaenuminjectedsources"></a>IDiaEnumInjectedSources
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举数据源中包含的各种插入的源。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaEnumInjectedSources : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaEnumInjectedSources`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaEnumInjectedSources::get__NewEnum](../../debugger/debug-interface-access/idiaenuminjectedsources-get-newenum.md)|检索[IEnumVARIANT 接口](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e)此枚举器的版本。|  
|[IDiaEnumInjectedSources::get_Count](../../debugger/debug-interface-access/idiaenuminjectedsources-get-count.md)|检索多个插入源。|  
|[IDiaEnumInjectedSources::Item](../../debugger/debug-interface-access/idiaenuminjectedsources-item.md)|通过索引中检索的插入的源。|  
|[IDiaEnumInjectedSources::Next](../../debugger/debug-interface-access/idiaenuminjectedsources-next.md)|检索指定的数目的枚举序列中的插入源。|  
|[IDiaEnumInjectedSources::Skip](../../debugger/debug-interface-access/idiaenuminjectedsources-skip.md)|跳过枚举序列中的插入源的指定的数目。|  
|[IDiaEnumInjectedSources::Reset](../../debugger/debug-interface-access/idiaenuminjectedsources-reset.md)|将枚举序列重置到开头。|  
|[IDiaEnumInjectedSources::Clone](../../debugger/debug-interface-access/idiaenuminjectedsources-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口通过调用[idiasession:: Findinjectedsource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)方法或通过调用特定的源文件的名称替换[idiasession:: Getenumtables](../../debugger/debug-interface-access/idiasession-getenumtables.md)方法使用的 GUID`IDiaEnumInjectedSources`接口。  
  
## <a name="example"></a>示例  
 此示例演示如何获取 (`GetEnumInjectedSources`函数)，并使用 (`DumpAllInjectedSources`函数)`IDiaEnumInjectedSources`接口。 请参阅[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)接口的实现`PrintPropertyStorage`函数。 备用输出，请参阅[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)接口。  
  
```cpp#  
  
IDiaEnumInjectedSources* GetEnumInjectedSources(IDiaSession *pSession)  
{  
    IDiaEnumInjectedSources* pUnknown    = NULL;  
    REFIID                   iid         = __uuidof(IDiaEnumInjectedSources);  
    IDiaEnumTables*          pEnumTables = NULL;  
    IDiaTable*               pTable      = NULL;  
    ULONG                    celt        = 0;  
  
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
  
void DumpAllInjectedSources( IDiaSession* pSession)  
{  
    IDiaEnumInjectedSources* pEnumInjSources;  
  
    pEnumInjSources = GetEnumInjectedSources(pSession);  
    if (pEnumInjSources != NULL)  
    {  
        IDiaInjectedSource* pInjSource;  
        ULONG celt = 0;  
  
        while(pEnumInjSources->Next(1, &pInjSource, &celt) == S_OK &&  
              celt == 1)  
        {  
            IDiaPropertyStorage *pPropertyStorage;  
            if (pInjSource->QueryInterface(__uuidof(IDiaPropertyStorage),  
                                           (void **)&pPropertyStorage) == S_OK)  
            {  
                PrintPropertyStorage(pPropertyStorage);  
                pPropertyStorage->Release();  
            }  
            pInjSource->Release();  
        }  
        pEnumInjSources->Release();  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)   
 [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)   
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)   
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
