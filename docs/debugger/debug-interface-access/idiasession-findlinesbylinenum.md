---
title: IDiaSession::findLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByLinenum method
ms.assetid: 76d5622d-9a91-4c2a-a98f-263af5d1daef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d5999febf6e926ef8e9beb365728a3b150e1a38
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839262"
---
# <a name="idiasessionfindlinesbylinenum"></a>IDiaSession::findLinesByLinenum
确定将编译单位在源文件中指定的行号位于内或附近的行号。

## <a name="syntax"></a>语法

```C++
HRESULT findLinesByLinenum ( 
    IDiaSymbol*           compiland,
    IDiaSourceFile*       file,
    DWORD                 linenum,
    DWORD                 column,
    IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
`compiland`

[in][IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)对象，表示要在其中搜索的行号编译单位。 此参数不能为 `NULL`。

`file`

[in][IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)对象，表示要在中搜索的源文件。 此参数不能为 `NULL`。

`linenum`

[in]指定基于 1 的行号。

> [!NOTE]
> 您不能使用零指定所有行 (使用[idiasession:: Findlines](../../debugger/debug-interface-access/idiasession-findlines.md)方法来查找所有行)。

`column`

[in]指定的列号。 使用零来指定所有列。 列是行的字节的偏移量。

`ppResult`

[out]返回[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) objta 包含的行号列表的检索。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何打开的源文件、 枚举提供此文件中，编译单位和每个编译单位的开始位置的源文件中找到的行号。

```C++
void ShowLinesInCompilands(IDiaSession *pSession, LPCOLESTR filename)
{
    IDiaEnumSourceFiles* pEnum;
    IDiaSourceFile*      pFile;
    DWORD                celt;

    pSession->findFile ( NULL, filename, nsFNameExt, &pEnum );
    while ( pEnum->Next ( 1, &pFile, &celt ) == S_OK ) // for each file
    {
        IDiaEnumSymbols* pEnumCompilands;
        IDiaSymbol* pCompiland;

        pFile->get_compilands ( &pEnumCompilands );
        // for each compiland
        while ( pEnumCompilands->Next ( 1, &pCompiland, &celt ) == S_OK )
        {
            IDiaEnumLineNumbers* pEnum;
            // Find first compiland closest to line 1 of the file.
            if (pSession->findLinesByLinenum( pCompiland, pFile, 1, 0, &pEnum ) == S_OK)
            {
                IDiaLineNumber *pLineNumber;
                DWORD lineCount;
                while ( pEnum->Next(1,&pLineNumber,&lineCount) == S_OK)
                {
                    DWORD lineNum;
                    if (pLineNumber->get_line(&lineNum) == S_OK)
                    {
                        printf("compiland starts in source at line number = %lu\n",lineNum);
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
