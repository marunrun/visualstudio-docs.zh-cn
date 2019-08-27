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
ms.openlocfilehash: 3a67dc121790acff1f5e39a82a1711317616fc2d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855042"
---
# <a name="querying-the-pdb-file"></a>查询 .Pdb 文件
程序数据库文件 (扩展名为.pdb) 是包含类型和符号化调试信息编译和链接项目的过程中收集的二进制文件。 在编译 C 时创建 PDB 文件 /C++带有程序 **/ZI**或 **/Zi**或[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]， [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]，或[!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)]带有程序 **/调试**选项。 对象文件包含到调试信息的.pdb 文件的引用。 Pdb 文件的详细信息，请参阅[PDB 文件](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100))。 DIA 应用程序可以使用以下常规步骤以获取有关各种符号、 对象和对可执行映像中的数据元素的详细信息。

### <a name="to-query-the-pdb-file"></a>查询.pdb 文件

1. 通过创建获得数据源[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)接口。

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

2. 调用[idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)或[idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)加载调试信息。

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

3. 调用[idiadatasource:: Opensession](../../debugger/debug-interface-access/idiadatasource-opensession.md)以打开[IDiaSession](../../debugger/debug-interface-access/idiasession.md)来获取调试信息的访问权限。

    ```C++
    CComPtr<IDiaSession> psession;
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
    ```

4. 使用中的方法`IDiaSession`查询数据源中的符号。

    ```C++
    CComPtr<IDiaSymbol> pglobal;
    if ( FAILED( psession->get_globalScope( &pglobal) ) )
    {
        Fatal( "get_globalScope" );
    }
    ```

5. 使用`IDiaEnum*`调试信息的接口枚举和浏览符号或其他元素。

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
