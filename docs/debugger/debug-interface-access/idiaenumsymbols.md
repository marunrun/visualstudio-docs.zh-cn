---
title: IDiaEnumSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols interface
ms.assetid: 649f7bfd-86ac-49a5-8533-aff77e1bc62e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0864522c079ff1f694072fec3147d006cd2ce43d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743899"
---
# <a name="idiaenumsymbols"></a>IDiaEnumSymbols
枚举数据源中包含的各种符号。

## <a name="syntax"></a>语法

```
IDiaEnumSymbols : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaEnumSymbols` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaEnumSymbols::get__NewEnum](../../debugger/debug-interface-access/idiaenumsymbols-get-newenum.md)|检索此枚举器的 `IEnumVARIANT Interface` 版本。|
|[IDiaEnumSymbols::get_Count](../../debugger/debug-interface-access/idiaenumsymbols-get-count.md)|检索符号数。|
|[IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)|通过索引检索符号。|
|[IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)|检索枚举序列中指定数目的符号。|
|[IDiaEnumSymbols::Skip](../../debugger/debug-interface-access/idiaenumsymbols-skip.md)|跳过枚举序列中指定数目的符号。|
|[IDiaEnumSymbols::Reset](../../debugger/debug-interface-access/idiaenumsymbols-reset.md)|将枚举序列重置到开始处。|
|[IDiaEnumSymbols::Clone](../../debugger/debug-interface-access/idiaenumsymbols-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|

## <a name="remarks"></a>备注
此接口提供按特定类型符号（例如 `SymTagUDT` （用户定义类型）或 `SymTagBaseClass` 进行分组的符号。 若要使用按地址分组的符号，请使用[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)接口。

## <a name="notes-for-callers"></a>调用方说明
通过调用以下方法获取此接口：

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)

## <a name="example"></a>示例
此示例演示如何获取 `IDiaEnumSymbols` 接口，然后使用该枚举来列出用户定义的类型（Udt）。

> [!NOTE]
> `CDiaBSTR` 是一个包装 `BSTR` 并在实例化超出范围时自动处理释放该字符串的类。

```C++
void ShowUDTs(IDiaSymbol *pGlobals)
{
    CComPtr<IDiaEnumSymbols> pEnum;
    CComPtr<IDiaSymbol> pSymbol;
    HRESULT hr;

    hr = pGlobals->findChildren(SymTagUDT,
                                NULL,
                                nsfCaseInsensitive | nsfUndecoratedName,
                                &pEnum);
    if (hr == S_OK)
    {
        while ( SUCCEEDED( hr = pEnum->Next( 1, &pSymbol, &celt ) ) &&
                celt == 1 )
        {
            CDiaBSTR name;
            if ( pSymbol->get_name( &name ) != S_OK )
                Fatal( "get_name" );
            printf( "Found UDT: %ws\n", name );
            pSymbol = 0;
        }
    }
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
