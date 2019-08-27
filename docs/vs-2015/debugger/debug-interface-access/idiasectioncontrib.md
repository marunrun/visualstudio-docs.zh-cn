---
title: IDiaSectionContrib | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib interface
ms.assetid: 371d40f6-ca0e-4d7e-9210-64d3768996c6
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fc263d7238166f4f381bac35f0482ca2433f7b33
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150479"
---
# <a name="idiasectioncontrib"></a>IDiaSectionContrib
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

描述了部分内容中检索数据，也就是说，连续内存块归功于图像编译单位。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaSectionContrib : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaSectionContrib`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaSectionContrib::get_compiland](../../debugger/debug-interface-access/idiasectioncontrib-get-compiland.md)|检索提供本部分的编译单位符号的引用。|  
|[IDiaSectionContrib::get_addressSection](../../debugger/debug-interface-access/idiasectioncontrib-get-addresssection.md)|检索的部分一部分发布内容的地址。|  
|[IDiaSectionContrib::get_addressOffset](../../debugger/debug-interface-access/idiasectioncontrib-get-addressoffset.md)|检索发布内容的地址的偏移量的部分。|  
|[IDiaSectionContrib::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasectioncontrib-get-relativevirtualaddress.md)|检索的映像相对虚拟地址 (RVA) 所占比例。|  
|[IDiaSectionContrib::get_virtualAddress](../../debugger/debug-interface-access/idiasectioncontrib-get-virtualaddress.md)|检索所占比例的虚拟地址 (VA)。|  
|[IDiaSectionContrib::get_length](../../debugger/debug-interface-access/idiasectioncontrib-get-length.md)|检索一个部分中的字节数。|  
|[IDiaSectionContrib::get_notPaged](../../debugger/debug-interface-access/idiasectioncontrib-get-notpaged.md)|检索一个标志，指示是否在部分不能换出内存。|  
|[IDiaSectionContrib::get_nopad](../../debugger/debug-interface-access/idiasectioncontrib-get-nopad.md)|检索一个标志，指示是否在部分应不填充到下一个内存边界。|  
|[IDiaSectionContrib::get_code](../../debugger/debug-interface-access/idiasectioncontrib-get-code.md)|检索一个标志，指示的部分是否包含可执行代码。|  
|[IDiaSectionContrib::get_code16bit](../../debugger/debug-interface-access/idiasectioncontrib-get-code16bit.md)|检索一个标志，指示的部分是否包含 16 位代码。|  
|[IDiaSectionContrib::get_initializedData](../../debugger/debug-interface-access/idiasectioncontrib-get-initializeddata.md)|检索一个标志，指示的部分是否包含初始化的数据。|  
|[IDiaSectionContrib::get_uninitializedData](../../debugger/debug-interface-access/idiasectioncontrib-get-uninitializeddata.md)|检索一个标志，指示的部分是否包含未初始化的数据。|  
|[IDiaSectionContrib::get_informational](../../debugger/debug-interface-access/idiasectioncontrib-get-informational.md)|检索一个标志，指示一个部分包含注释或类似的信息。|  
|[IDiaSectionContrib::get_remove](../../debugger/debug-interface-access/idiasectioncontrib-get-remove.md)|检索一个标志，指示它进行内存中映像的一部分之前是否删除节。|  
|[IDiaSectionContrib::get_comdat](../../debugger/debug-interface-access/idiasectioncontrib-get-comdat.md)|检索一个标志，指示了 COMDAT 记录的部分。|  
|[IDiaSectionContrib::get_discardable](../../debugger/debug-interface-access/idiasectioncontrib-get-discardable.md)|检索一个标志，指示是否可以放弃部分。|  
|[IDiaSectionContrib::get_notCached](../../debugger/debug-interface-access/idiasectioncontrib-get-notcached.md)|检索一个标志，指示是否不能缓存部分。|  
|[IDiaSectionContrib::get_share](../../debugger/debug-interface-access/idiasectioncontrib-get-share.md)|检索一个标志，指示是否可以在内存中共享部分。|  
|[IDiaSectionContrib::get_execute](../../debugger/debug-interface-access/idiasectioncontrib-get-execute.md)|检索一个标志，指示是否可执行文件作为代码部分。|  
|[IDiaSectionContrib::get_read](../../debugger/debug-interface-access/idiasectioncontrib-get-read.md)|检索一个标志，指示是否可以读取部分。|  
|[IDiaSectionContrib::get_write](../../debugger/debug-interface-access/idiasectioncontrib-get-write.md)|检索一个标志，指示是否可以写入部分。|  
|[IDiaSectionContrib::get_dataCrc](../../debugger/debug-interface-access/idiasectioncontrib-get-datacrc.md)|检索的部分中的数据的循环冗余检查 (CRC)。|  
|[IDiaSectionContrib::get_relocationsCrc](../../debugger/debug-interface-access/idiasectioncontrib-get-relocationscrc.md)|检索部分中的重定位信息的 CRC。|  
|[IDiaLineNumber::get_compilandId](../../debugger/debug-interface-access/idialinenumber-get-compilandid.md)|检索部分的编译单位标识符。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口通过调用[idiaenumsectioncontribs:: Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)并[idiaenumsectioncontribs:: Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)方法。 请参阅[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)接口以举例说明获取`IDiaSectionContrib`接口。  
  
## <a name="example"></a>示例  
 此函数显示每个部分以及任何关联的符号的地址。 请参阅[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)接口，以查看如何`IDiaSectionContrib`获取接口。  
  
```cpp#  
void PrintSectionContrib(IDiaSectionContrib* pSecContrib, IDiaSession* pSession)  
{  
    if (pSecContrib != NULL && pSession != NULL)  
    {  
        DWORD rva;  
        if ( pSecContrib->get_relativeVirtualAddress( &rva ) == S_OK )  
        {  
            printf( "\taddr: 0x%.8X", rva );  
            pSecContrib = NULL;  
            CComPtr<IDiaSymbol> pSym;  
            if ( psession->findSymbolByRVA( rva, SymTagNull, &pSym ) == S_OK )  
            {  
                CDiaBSTR name;  
                DWORD    tag;  
                pSym->get_symTag( &tag );  
                pSym->get_name( &name );  
                printf( "     symbol: %ws (%ws)\n",  
                        name != NULL ? name : L"",  
                        szTags[ tag ] );  
            }  
            else  
            {  
                printf( "<no symbol found?>\n" );  
            }  
        }  
        else  
        {  
            DWORD isect;  
            DWORD offset;  
            pSecContrib->get_addressSection( &isect );  
            pSecContrib->get_addressOffset( &offset );  
            printf( "\taddr: 0x%.4X:0x%.8X", isect, offset );  
            pSecContrib = NULL;  
            CComPtr<IDiaSymbol> pSym;  
            if ( SUCCEEDED( psession->findSymbolByAddr(  
                                              isect,  
                                              offset,  
                                              SymTagNull,  
                                              &pSym )  
                          )  
               )  
            {  
                CDiaBSTR name;  
                DWORD    tag;  
                pSym->get_symTag( &tag );  
                pSym->get_name( &name );  
                printf( "     symbol: %ws (%ws)\n",  
                    name != NULL ? name : L"",  
                    szTags[ tag ] );  
            }  
            else  
            {  
                printf( "<no symbol found?>\n" );  
            }  
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
 [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)   
 [IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)   
 [IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)
