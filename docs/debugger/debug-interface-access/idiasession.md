---
title: IDiaSession | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f983275974ed0ec3fb0e6091f5b9e73cdccd76ef
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741858"
---
# <a name="idiasession"></a>IDiaSession
提供调试符号的查询上下文。

## <a name="syntax"></a>语法

```
IDiaSession : IUnknown
```

## <a name="methods"></a>方法
下表显示 `IDiaSession` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|检索对应于此符号存储区中的符号的可执行文件的加载地址。 这与传递到 `put_loadAddress` 方法的值相同。|
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|设置与此符号存储区中的符号对应的可执行文件的加载地址。 **注意：** 当你获取 `IDiaSession` 对象和开始使用对象之前，请务必调用此方法。|
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|检索对全局范围的引用。|
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|检索符号存储区中包含的所有表的枚举器。|
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|检索静态位置的所有命名符号的枚举器。|
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|检索与名称和符号类型匹配的指定父标识符的所有子级。|
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|检索指定地址中包含或最近的指定符号类型。|
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|检索指定的符号类型，该类型包含指定的相对虚拟地址（RVA），或该类型最接近指定的相对虚拟地址（RVA）。|
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|检索指定的符号类型，该类型包含指定的虚拟地址（VA），或该类型最接近指定的虚拟地址。|
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|检索包含指定的元数据标记的符号。|
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|检查两个符号是否等效。|
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|按其唯一标识符检索符号。|
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|检索指定的符号类型，该类型包含或最接近于指定的相对虚拟地址和偏移量。|
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|检索指定的符号类型，该类型包含或最近指定的虚拟地址和偏移量。|
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|按编译单位和名称检索源文件。|
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|按源文件标识符检索源文件。|
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|检索指定编译单位和源文件标识符中的行号。|
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|检索指定编译单位中包含指定地址的行。|
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|检索指定编译单位中包含指定的相对虚拟地址的行。|
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|查找指定地址范围内所包含行的行号信息。|
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|按源文件和行号检索指定编译单位中的行。|
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|检索由特性提供程序或编译过程的其他组件放入到符号存储区中的源。|
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|检索调试数据流的枚举序列。|
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|检索一个枚举，该枚举允许客户端遍历给定地址的所有内联帧。|
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|检索允许客户端循环访问指定的相对虚拟地址（RVA）上所有内联帧的枚举。|
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|检索一个枚举，该枚举允许客户端循环访问指定虚拟地址（VA）上的所有内联帧。|
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|检索一个枚举，该枚举允许客户端循环访问由指定的父符号直接或间接内联的所有函数的行号信息。|
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|检索一个枚举，该枚举允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息，并将其包含在指定的地址范围内。|
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|检索一个枚举，该枚举允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息，并将其包含在指定的相对虚拟地址（RVA）中。|
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|检索一个枚举，该枚举允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息，并将其包含在指定的虚拟地址（VA）中。|
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|检索一个枚举，该枚举允许客户端循环访问指定源文件和行号内直接或间接内联的所有函数的行号信息。|
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|检索一个枚举，该枚举允许客户端循环访问与指定名称匹配的所有内联函数的行号信息。|
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|对于指定的标记值对应于父加速器存根函数中的变量，返回其符号的枚举。|
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|给定相应的标记值后，此方法将返回一个符号枚举，其中包含在指定的相对虚拟地址处的指定父加速器存根函数中。|
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|返回与指定内联函数名称对应的内联帧的符号的枚举。|
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|返回与指定源位置对应的内联帧的符号枚举。|

## <a name="remarks"></a>备注
在创建 `IDiaSession` 对象后调用[IDiaSession：:P ut_loadaddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)方法（并且传递到 `put_loadAddress` 方法的值必须为非零）非常重要，这是为了能够访问符号的任何虚拟地址（VA）属性。 加载地址来自要调试的可执行文件加载的任何程序。 例如，如果给定可执行文件的句柄，则可以调用 Win32 函数 `GetModuleInformation` 来检索可执行文件的加载地址。

## <a name="example"></a>示例
此示例演示如何在 DIA SDK 的常规初始化过程中获取 `IDiaSession` 接口。

```C++
CComPtr<IDiaDataSource> pSource;
ComPtr<IDiaSession> psession;

void InitializeDIA(const char *szFilename)
{
    HRESULT hr = CoCreateInstance( CLSID_DiaSource,
                                   NULL,
                                   CLSCTX_INPROC_SERVER,
                                   __uuidof( IDiaDataSource ),
                                  (void **) &pSource);
    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename,
              szFilename,
              sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [Exe](../../debugger/debug-interface-access/exe.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
- [查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
