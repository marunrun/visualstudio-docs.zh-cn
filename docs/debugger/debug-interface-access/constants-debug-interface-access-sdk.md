---
title: 常量（调试接口访问 SDK） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- constants, DIA SDK
- DIA SDK, constants
ms.assetid: aca4ec77-bc08-4cdd-a6ce-8d4a28ea5ea3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b10ab87f056bc153ec41c125b0e01ddefa139b80
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745404"
---
# <a name="constants-debug-interface-access-sdk"></a>常量（调试接口访问 SDK）
这些字符串常量可用于通过 DIA SDK 标识程序调试数据库（PDB）文件的各个部分。

## <a name="constants"></a>常量
以下声明为 C/C++宏。

|宏|“值”|
|-----------|-----------|
|`DiaTable_Symbols`|L "符号"|
|`DiaTable_Sections`|L "Sections"|
|`DiaTable_SrcFiles`|L "SourceFiles"|
|`DiaTable_LineNums`|L"LineNumbers"|
|`DiaTable_SegMap`|L"SegmentMap"|
|`DiaTable_Dbg`|L"Dbg"|
|`DiaTable_InjSrc`|L "InjectedSource"|
|`DiaTable_FrameData`|L"FrameData"|

## <a name="example"></a>示例
下面是一个使用以下符号的示例：

```C++
HRESULT GetSymbolTable(IDiaEnumTables *pEnumTables, IDiaTable **pTable)
{
    HRESULT hr;
    VARIANT var;
    var.vt      = VT_BSTR;
    var.bstrVal = SysAllocString( DiaTable_Symbols );
    hr = pEnumTables->Item( var, pTable );
    return(hr);
}
```

## <a name="requirements"></a>要求
标头： dia2

## <a name="see-also"></a>请参阅
- [引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
