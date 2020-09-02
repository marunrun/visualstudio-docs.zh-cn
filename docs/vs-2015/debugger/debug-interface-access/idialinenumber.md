---
title: IDiaLineNumber | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber interface
ms.assetid: 1071f7d0-1f8c-4384-933f-c49c7eb930bd
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d39a5ccc130af3281fad305e75690d906bdfa4ad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62535523"
---
# <a name="idialinenumber"></a>IDiaLineNumber
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

访问描述从图像的字节块到源文件行号的映射过程的信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaLineNumber : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDiaLineNumber` 。  
  
|方法|说明|  
|------------|-----------------|  
|[IDiaLineNumber::get_compiland](../../debugger/debug-interface-access/idialinenumber-get-compiland.md)|检索提供图像文本字节的编译单位的符号引用。|  
|[IDiaLineNumber::get_sourceFile](../../debugger/debug-interface-access/idialinenumber-get-sourcefile.md)|检索对源文件对象的引用。|  
|[IDiaLineNumber::get_lineNumber](../../debugger/debug-interface-access/idialinenumber-get-linenumber.md)|检索源文件中的行号。|  
|[IDiaLineNumber::get_lineNumberEnd](../../debugger/debug-interface-access/idialinenumber-get-linenumberend.md)|检索语句或表达式结束处的源行号（从1开始）。|  
|[IDiaLineNumber::get_columnNumber](../../debugger/debug-interface-access/idialinenumber-get-columnnumber.md)|检索表达式或语句开始的列号。|  
|[IDiaLineNumber::get_columnNumberEnd](../../debugger/debug-interface-access/idialinenumber-get-columnnumberend.md)|检索表达式或语句结束的列号。|  
|[IDiaLineNumber::get_addressSection](../../debugger/debug-interface-access/idialinenumber-get-addresssection.md)|检索内存地址中某个块开始的部分。|  
|[IDiaLineNumber::get_addressOffset](../../debugger/debug-interface-access/idialinenumber-get-addressoffset.md)|检索内存地址中某个块开始处的偏移量部分。|  
|[IDiaLineNumber::get_relativeVirtualAddress](../../debugger/debug-interface-access/idialinenumber-get-relativevirtualaddress.md)|检索块 (RVA) 的映像相对虚拟地址。|  
|[IDiaLineNumber::get_virtualAddress](../../debugger/debug-interface-access/idialinenumber-get-virtualaddress.md)|检索块 (VA) 的虚拟地址。|  
|[IDiaLineNumber::get_length](../../debugger/debug-interface-access/idialinenumber-get-length.md)|检索块中的字节数。|  
|[IDiaLineNumber::get_sourceFileId](../../debugger/debug-interface-access/idialinenumber-get-sourcefileid.md)|检索提供此行的源文件的唯一源文件标识符。|  
|[IDiaLineNumber::get_statement](../../debugger/debug-interface-access/idialinenumber-get-statement.md)|检索一个标志，该标志指示此行信息描述程序源中语句的开头。|  
|[IDiaLineNumber::get_compilandId](../../debugger/debug-interface-access/idialinenumber-get-compilandid.md)|检索提供此行的编译单位的唯一标识符。|  
  
## <a name="remarks"></a>备注  
  
## <a name="notes-for-callers"></a>调用方说明  
 通过调用 [IDiaEnumLineNumbers：： Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md) 或 [IDiaEnumLineNumbers：： Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md) 方法获取此接口。  
  
## <a name="example"></a>示例  
 下面的函数显示) 所表示的函数 (中使用的行号 `pSymbol` 。  
  
```cpp#  
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
 标头： Dia2  
  
 库： diaguids  
  
 DLL： msdia80.dll  
  
## <a name="see-also"></a>另请参阅  
 [接口 (调试接口访问 SDK) ](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)   
 [IDiaEnumLineNumbers：： Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)   
 [IDiaEnumLineNumbers::Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md)
