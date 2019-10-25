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
ms.openlocfilehash: bc7a573eb92d7c51079b0a7e97067abd155ae4fa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738711"
---
# <a name="idiatable"></a>IDiaTable
枚举 DIA 数据源表。

## <a name="syntax"></a>语法

```
IDiaTable : IEnumUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaTable` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|检索此枚举器的[IEnumVARIANT 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant)版本。|
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|检索表的名称。|
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|检索表中的项数。|
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|检索对特定项索引的引用。|

## <a name="remarks"></a>备注
此接口实现 VisualStudio 命名空间中的 `IEnumUnknown` 枚举方法。 与[IDiaTable：： get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)和[IDiaTable：： Item](../../debugger/debug-interface-access/idiatable-item.md)方法相比，要循环访问表内容，`IEnumUnknown` 枚举接口要高效得多。

从 `IDiaTable::Item` 方法或 `Next` 方法（VisualStudio 命名空间）中返回的 `IUnknown` 接口的解释依赖于表的类型的解释。 例如，如果 `IDiaTable` 接口表示注入的源的列表，则应为[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)接口查询 `IUnknown` 接口。

## <a name="notes-for-callers"></a>调用方说明
通过调用[IDiaEnumTables：： Item](../../debugger/debug-interface-access/idiaenumtables-item.md)或[IDiaEnumTables：： Next](../../debugger/debug-interface-access/idiaenumtables-next.md)方法获取此接口。

下面的接口是通过 `IDiaTable` 接口实现的（也就是说，你可以查询以下接口之一的 `IDiaTable` 接口）：

- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

## <a name="example"></a>示例
第一个函数 `ShowTableNames` 显示会话中所有表的名称。 @No__t_0 的第二个函数在表中搜索实现指定接口的所有表。 @No__t_0 的第三个函数演示如何使用 `GetTable` 函数。

> [!NOTE]
> `CDiaBSTR` 是一个包装 `BSTR` 并在实例化超出范围时自动处理释放该字符串的类。

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
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
- [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
