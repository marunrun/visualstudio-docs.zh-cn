---
title: IDiaTable | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5b9c9f85ffbf4eed2fdc305a64bd3f32822dacd6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682792"
---
# <a name="idiatable"></a>IDiaTable
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

枚举 DIA 数据源表。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaTable : IEnumUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDiaTable` 。  
  
|方法|说明|  
|------------|-----------------|  
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|检索此枚举器的 [IEnumVARIANT 接口](https://msdn.microsoft.com/139e3c93-faef-4003-9079-e0e94494db3e) 版本。|  
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|检索表的名称。|  
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|检索表中的项数。|  
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|检索对特定项索引的引用。|  
  
## <a name="remarks"></a>备注  
 此接口实现 `IEnumUnknown` VisualStudio 命名空间中的枚举方法。 `IEnumUnknown`枚举接口比[IDiaTable：： Get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)和[IDiaTable：： Item](../../debugger/debug-interface-access/idiatable-item.md)方法循环访问表内容更有效。  
  
 `IUnknown`从 `IDiaTable::Item` VisualStudio 命名空间) 中的方法或 (方法返回的接口的解释 `Next` 取决于表的类型。 例如，如果 `IDiaTable` 接口表示注入的源的列表，则应为 `IUnknown` [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) 接口查询接口。  
  
## <a name="notes-for-callers"></a>调用方说明  
 通过调用 [IDiaEnumTables：： Item](../../debugger/debug-interface-access/idiaenumtables-item.md) 或 [IDiaEnumTables：： Next](../../debugger/debug-interface-access/idiaenumtables-next.md) 方法获取此接口。  
  
 下面的接口是通过 `IDiaTable` 接口 (实现的，你可以在接口中查询 `IDiaTable` 以下某个接口) ：  
  
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)  
  
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)  
  
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)  
  
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)  
  
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)  
  
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)  
  
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)  
  
## <a name="example"></a>示例  
 第一个函数 `ShowTableNames` 显示会话中所有表的名称。 第二个函数在表 `GetTable` 中搜索实现指定接口的所有表。 第三个函数 `UseTable` 演示如何使用 `GetTable` 函数。  
  
> [!NOTE]
> `CDiaBSTR` 是一个类，在 `BSTR` 实例化超出范围时，它会自动处理释放字符串。  
  
```cpp#  
void ShowTableNames(IDiaSession *pSession)  
{  
    CComPtr<IDiaEnumTables> pTables;  
    if ( FAILED( psession->getEnumTables( &pTables ) ) )  
    {  
        Fatal( "getEnumTables" );  
    }  
    CComPtr< IDiaTable > pTable;  
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) )  
            && celt == 1 )  
    {  
        CDiaBSTR bstrTableName;  
        if ( pTable->get_name( &bstrTableName ) != 0 )  
        {  
            Fatal( "get_name" );  
        }  
        printf( "Found table: %ws\n", bstrTableName );  
    }  
  
// Searches the list of all tables for a table that supports  
// the specified interface.  Use this function to obtain an  
// enumeration interface.  
HRESULT GetTable(IDiaSession* pSession,  
                 REFIID       iid,  
                 void**       ppUnk)  
{  
    CComPtr<IDiaEnumTables> pEnumTables;  
    HRESULT hResult;  
  
    if (FAILED(pSession->getEnumTables(&pEnumTables)))  
        Fatal("getEnumTables");  
  
    CComPtr<IDiaTable> pTable;  
    ULONG celt = 0;  
    while (SUCCEEDED(hResult = pEnumTables->Next(1, &pTable, &celt)) &&  
           celt == 1)  
    {  
        if (pTable->QueryInterface(iid, (void**)ppUnk) == S_OK)  
        {  
            return S_OK;  
        }  
        pTable = NULL;  
    }  
  
    if (FAILED(hResult))  
        Fatal("EnumTables->Next");  
  
    return E_FAIL;  
}  
  
// This function shows how to use the GetTable function.  
void UseTable(IDiaSession *pSession)  
{  
    CComPtr<IDiaEnumSegments> pEnumSegments;  
    if (SUCCEEDED(GetTable(pSession, __uuidof(IDiaEnumSegments), &pEnumSegments)))  
    {  
        // Do something with pEnumSegments.  
    }  
}  
```  
  
## <a name="requirements"></a>要求  
 标头： Dia2  
  
 库： diaguids  
  
 DLL： msdia80.dll  
  
## <a name="see-also"></a>另请参阅  
 [接口 (调试接口访问 SDK) ](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)   
 [IDiaEnumTables：： Item](../../debugger/debug-interface-access/idiaenumtables-item.md)   
 [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
