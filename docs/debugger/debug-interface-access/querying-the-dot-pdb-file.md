---
title: 查询。Pdb 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68efbd59abe1b0aff717a55383f3ac330586164a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738582"
---
# <a name="querying-the-pdb-file"></a>查询 .Pdb 文件
程序数据库文件（扩展名 .pdb）是一个二进制文件，其中包含在编译和链接项目的过程中收集的类型和符号调试信息。 当使用 **/zi**或 **/zi**或使用 **/debug**选项的 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]C++ 、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 程序编译 C/程序时，将创建 PDB 文件。 对于调试信息，对象文件包含对 .pdb 文件的引用。 有关 pdb 文件的详细信息，请参阅[Pdb 文件](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100))。 DIA 应用程序可以使用以下常规步骤来获取有关可执行映像中各种符号、对象和数据元素的详细信息。

### <a name="to-query-the-pdb-file"></a>查询 .pdb 文件

1. 通过创建[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)接口获取数据源。

    ```C++
    CComPtr<IDiaDataSource> pSource;
    hr = CoCreateInstance( CLSID_DiaSource,
                           NULL,
                           CLSCTX_INPROC_SERVER,
                           __uuidof( IDiaDataSource ),
                          (void **) &pSource);

    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    ```

2. 调用[IDiaDataSource：： loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)或[IDiaDataSource：： loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)加载调试信息。

    ```C++
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename, szFilename, sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    ```

3. 调用[IDiaDataSource：： openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)以打开[IDiaSession](../../debugger/debug-interface-access/idiasession.md)以获取对调试信息的访问。

    ```C++
    CComPtr<IDiaSession> psession;
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
    ```

4. 使用 `IDiaSession` 中的方法来查询数据源中的符号。

    ```C++
    CComPtr<IDiaSymbol> pglobal;
    if ( FAILED( psession->get_globalScope( &pglobal) ) )
    {
        Fatal( "get_globalScope" );
    }
    ```

5. 使用 `IDiaEnum*` 接口来枚举和扫描调试信息的符号或其他元素。

    ```C++
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) ) && celt == 1 )
    {
        // Do something with each IDiaTable.
    }
    ```

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
