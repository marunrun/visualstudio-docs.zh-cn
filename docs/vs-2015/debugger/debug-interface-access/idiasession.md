---
title: IDiaSession | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 002e7198210e123fc2461f712bb8db442b9f25c8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190718"
---
# <a name="idiasession"></a>IDiaSession
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

提供调试符号的查询上下文。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaSession : IUnknown  
```  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDiaSession`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|检索对应于此符号存储区中的符号的可执行文件的加载地址。 这是相同的值传递给`put_loadAddress`方法。|  
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|此符号存储区中的符号设置相对应的可执行文件的加载地址。 **注意：** 务必要调用此方法时，获取`IDiaSession`对象，并开始使用该对象之前。|  
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|检索对全局范围内的引用。|  
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|检索包含在符号存储区中的所有表的枚举器。|  
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|检索静态位置上的所有命名符号的枚举的器。|  
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|检索指定的父标识符相匹配的名称和符号类型的所有子级。|  
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|检索包含，或与指定的地址最接近的指定的符号类型。|  
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|检索包含，或与指定的相对虚拟地址 (RVA) 最接近的指定的符号类型。|  
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|检索包含，或与指定的虚拟地址 (VA) 最接近的指定的符号类型。|  
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|检索包含指定元数据标记的符号。|  
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|检查以查看两个符号是否等效。|  
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|检索由其唯一标识符的符号。|  
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|检索包含，或与指定的相对虚拟地址和偏移量最接近的指定的符号类型。|  
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|检索包含，或与指定的虚拟地址和偏移量最接近的指定的符号类型。|  
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|检索由编译单位和名称的源文件。|  
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|按源文件标识符检索源文件。|  
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|检索指定的编译单位和源代码文件标识符中的行号。|  
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|检索包含指定的地址的行中指定的编译单位。|  
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|检索包含指定的相对虚拟地址的行中指定的编译单位。|  
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|查找指定的地址范围中包含行的行号信息。|  
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|检索由源文件和行号指定编译单位中的行。|  
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|检索已放入符号存储区的属性提供者或其他组件在编译过程的源。|  
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|检索一个枚举的调试数据流的序列。|  
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|检索一个枚举，允许客户端用于循环访问所有给定地址上的内联框架。|  
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|检索一个枚举，允许客户端用于循环访问所有指定的相对虚拟地址 (RVA) 上的内联框架。|  
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|检索一个枚举，允许客户端用于循环访问所有指定的虚拟地址 (VA) 上的内联框架。|  
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|检索一个枚举，允许客户端来循环访问的所有函数的内联，直接或间接地，由指定的父符号的行号信息。|  
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|检索一个枚举，它允许客户端可以循环访问的所有函数的内联，直接或间接地，由指定的父符号的行号信息且包含在指定的地址范围。|  
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|检索一个枚举，它允许客户端可以循环访问的所有函数的内联，直接或间接地，由指定的父符号的行号信息且包含在指定的相对虚拟地址 (RVA)。|  
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|检索一个枚举，它允许客户端可以循环访问的所有函数的内联，直接或间接地，由指定的父符号的行号信息且包含在指定的虚拟地址 (VA)。|  
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|检索一个枚举，允许客户端进行循环访问，将内联，直接或间接指定的源文件和行号中的所有函数的行号信息。|  
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|检索一个枚举，允许客户端来循环访问的所有内联函数的指定的名称匹配的行号信息。|  
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|在父 Accelerator 存根 （stub） 函数中返回指定的标记值对应于该变量的符号的枚举。|  
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|提供相应的标记值，则此方法将返回在指定的父 Accelerator 存根 （stub） 函数在指定的相对虚拟地址中包含的符号的枚举。|  
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|返回与指定为内联函数名称相对应的内嵌帧的符号的枚举。|  
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|返回指定的源位置相对应的内嵌帧的符号的枚举。|  
  
## <a name="remarks"></a>备注  
 务必要调用[idiasession:: Put_loadaddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)方法创建后的`IDiaSession`对象 — 和值传递给`put_loadAddress`方法必须为非零 — 的符号为任何虚拟地址 (VA) 属性可访问。 加载地址来自于任何程序加载正在调试的可执行文件。 例如，可以调用 Win32 函数`GetModuleInformation`来检索可执行文件，加载地址提供给可执行文件的句柄。  
  
## <a name="example"></a>示例  
 此示例演示如何获取`IDiaSession`接口作为 DIA SDK 的常规初始化的一部分。  
  
```cpp#  
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
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [Exe](../../debugger/debug-interface-access/exe.md)   
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)   
 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)   
 [查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
