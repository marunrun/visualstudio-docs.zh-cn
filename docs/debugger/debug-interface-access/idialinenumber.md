---
title: IDiaLineNumber | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber interface
ms.assetid: 1071f7d0-1f8c-4384-933f-c49c7eb930bd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 327a53a28e5b37d33d44375653c1bffa56c7ddd2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829029"
---
# <a name="idialinenumber"></a>IDiaLineNumber
介绍从图像的文字字节块映射到源文件行号的过程的访问信息。

## <a name="syntax"></a>语法

```
IDiaLineNumber : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaLineNumber`。

|方法|描述|
|------------|-----------------|
|[IDiaLineNumber::get_compiland](../../debugger/debug-interface-access/idialinenumber-get-compiland.md)|检索对提供的图像的文字的字节将编译单位符号的引用。|
|[IDiaLineNumber::get_sourceFile](../../debugger/debug-interface-access/idialinenumber-get-sourcefile.md)|检索对源文件对象的引用。|
|[IDiaLineNumber::get_lineNumber](../../debugger/debug-interface-access/idialinenumber-get-linenumber.md)|检索源文件中的行号。|
|[IDiaLineNumber::get_lineNumberEnd](../../debugger/debug-interface-access/idialinenumber-get-linenumberend.md)|检索的语句或表达式的结束位置的基于 1 的源行号。|
|[IDiaLineNumber::get_columnNumber](../../debugger/debug-interface-access/idialinenumber-get-columnnumber.md)|检索表达式或语句的开始处的列号。|
|[IDiaLineNumber::get_columnNumberEnd](../../debugger/debug-interface-access/idialinenumber-get-columnnumberend.md)|检索表达式或语句的结束位置的列号。|
|[IDiaLineNumber::get_addressSection](../../debugger/debug-interface-access/idialinenumber-get-addresssection.md)|检索一个块的开始处的内存地址的部分部分。|
|[IDiaLineNumber::get_addressOffset](../../debugger/debug-interface-access/idialinenumber-get-addressoffset.md)|检索一个块的开始处的内存地址的偏移量的部分。|
|[IDiaLineNumber::get_relativeVirtualAddress](../../debugger/debug-interface-access/idialinenumber-get-relativevirtualaddress.md)|检索图像相对虚拟地址 (RVA) 的块。|
|[IDiaLineNumber::get_virtualAddress](../../debugger/debug-interface-access/idialinenumber-get-virtualaddress.md)|检索一个块的虚拟地址 (VA)。|
|[IDiaLineNumber::get_length](../../debugger/debug-interface-access/idialinenumber-get-length.md)|检索在块中的字节数。|
|[IDiaLineNumber::get_sourceFileId](../../debugger/debug-interface-access/idialinenumber-get-sourcefileid.md)|检索唯一的源文件标识符提供此行的源文件。|
|[IDiaLineNumber::get_statement](../../debugger/debug-interface-access/idialinenumber-get-statement.md)|检索一个标志，指示此行信息描述程序源中的语句的开头。|
|[IDiaLineNumber::get_compilandId](../../debugger/debug-interface-access/idialinenumber-get-compilandid.md)|检索提供此行将编译单位的唯一标识符。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方的说明
通过调用来获取此接口[idiaenumlinenumbers:: Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)或[idiaenumlinenumbers:: Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md)方法。

## <a name="example"></a>示例
以下函数显示在函数中使用的行号 (由`pSymbol`)。

```C++
void dumpFunctionLines( IDiaSymbol* pSymbol, IDiaSession* pSession )
{
    ULONGLONG length = 0;
    DWORD     isect  = 0;
    DWORD     offset = 0;

    pSymbol->get_addressSection( &isect );
    pSymbol->get_addressOffset( &offset );
    pSymbol->get_length( &length );
    if ( isect != 0 && length > 0 )
    {
        CComPtr< IDiaEnumLineNumbers > pLines;
        if ( SUCCEEDED( pSession->findLinesByAddr(
                                      isect,
                                      offset,
                                      static_cast<DWORD>( length ),
                                      &pLines)
                      )
           )
        {
            CComPtr< IDiaLineNumber > pLine;
            DWORD celt      = 0;
            bool  firstLine = true;

            while ( SUCCEEDED( pLines->Next( 1, &pLine, &celt ) ) &&
                    celt == 1 )
            {
                DWORD offset;
                DWORD seg;
                DWORD linenum;
                CComPtr< IDiaSymbol >     pComp;
                CComPtr< IDiaSourceFile > pSrc;

                pLine->get_compiland( &pComp );
                pLine->get_sourceFile( &pSrc );
                pLine->get_addressSection( &seg );
                pLine->get_addressOffset( &offset );
                pLine->get_lineNumber( &linenum );
                printf( "\tline %d at 0x%x:0x%x\n", linenum, seg, offset );
                pLine = NULL;
                if ( firstLine )
                {
                    // sanity check
                    CComPtr< IDiaEnumLineNumbers > pLinesByLineNum;
                    if ( SUCCEEDED( pSession->findLinesByLinenum(
                                                  pComp,
                                                  pSrc,
                                                  linenum,
                                                  0,
                                                  &pLinesByLineNum)
                                  )
                       )
                    {
                        CComPtr< IDiaLineNumber > pLine;
                        DWORD celt;
                        while ( SUCCEEDED( pLinesByLineNum->Next( 1, &pLine, &celt ) ) &&
                                celt == 1 )
                        {
                            DWORD offset;
                            DWORD seg;
                            DWORD linenum;

                            pLine->get_addressSection( &seg );
                            pLine->get_addressOffset( &offset );
                            pLine->get_lineNumber( &linenum );
                            printf( "\t\tfound line %d at 0x%x:0x%x\n", linenum, seg, offset );
                            pLine = NULL;
                        }
                    }
                    firstLine = false;
                }
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
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaEnumLineNumbers::Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)
- [IDiaEnumLineNumbers::Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md)
