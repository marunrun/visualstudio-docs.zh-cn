---
title: IDiaTable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 604c68ef82f66358238f94b43f000fae24a076f1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834147"
---
# <a name="idiatable"></a>IDiaTable
枚举 DIA 数据源表。

## <a name="syntax"></a>语法

```
IDiaTable : IEnumUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaTable`。

|方法|描述|
|------------|-----------------|
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|检索[IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)此枚举器的版本。|
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|检索表的名称。|
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|检索表中的项的数目。|
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|检索特定项索引的引用。|

## <a name="remarks"></a>备注
此接口实现`IEnumUnknown`Microsoft.VisualStudio.OLE.Interop 命名空间中的枚举方法。 `IEnumUnknown`枚举接口是用于循环访问表的内容相比要高效得多[idiatable:: Get_count](../../debugger/debug-interface-access/idiatable-get-count.md)并[idiatable:: Item](../../debugger/debug-interface-access/idiatable-item.md)方法。

解释`IUnknown`接口返回眖`IDiaTable::Item`方法或`Next`（位于 Microsoft.VisualStudio.OLE.Interop 命名空间） 的方法是依赖于表的类型。 例如，如果`IDiaTable`接口表示的插入源列表`IUnknown`应为查询接口[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)接口。

## <a name="notes-for-callers"></a>调用方的说明
通过调用来获取此接口[idiaenumtables:: Item](../../debugger/debug-interface-access/idiaenumtables-item.md)或[idiaenumtables:: Next](../../debugger/debug-interface-access/idiaenumtables-next.md)方法。

在实现以下接口`IDiaTable`接口 (即，您可以查询`IDiaTable`界面为以下接口之一):

- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

## <a name="example"></a>示例
第一个函数， `ShowTableNames`，在会话中显示的所有表的名称。 第二个函数， `GetTable`，搜索所有实现指定的接口的表的表。 第三个函数， `UseTable`，演示如何使用`GetTable`函数。

> [!NOTE]
> `CDiaBSTR` 是一个类，包装`BSTR`和实例化超出范围时释放该字符串将自动处理。

```C++
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
标头：dia2.h

库： diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
- [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
