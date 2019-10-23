---
title: IDiaSegment | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSegment interface
ms.assetid: 384ae0e1-077e-4d4f-98de-ac43c32c882f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 855b40f3d35d884a366e8fdc36ed1ec4f2bef85a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742341"
---
# <a name="idiasegment"></a>IDiaSegment
将数据从节号映射到地址空间的段。

## <a name="syntax"></a>语法

```
IDiaSegment : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaSegment` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaSegment::get_frame](../../debugger/debug-interface-access/idiasegment-get-frame.md)|检索段号。|
|[IDiaSegment::get_offset](../../debugger/debug-interface-access/idiasegment-get-offset.md)|检索节开始处的偏移量。|
|[IDiaSegment::get_length](../../debugger/debug-interface-access/idiasegment-get-length.md)|检索段中的字节数。|
|[IDiaSegment::get_read](../../debugger/debug-interface-access/idiasegment-get-read.md)|检索一个标志，该标志指示是否可以读取段。|
|[IDiaSegment::get_write](../../debugger/debug-interface-access/idiasegment-get-write.md)|检索一个标志，该标志指示是否可以修改段。|
|[IDiaSegment::get_execute](../../debugger/debug-interface-access/idiasegment-get-execute.md)|检索一个标志，该标志指示段是否可执行。|
|[IDiaSegment::get_addressSection](../../debugger/debug-interface-access/idiasegment-get-addresssection.md)|检索映射到此段的节号。|
|[IDiaSegment::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasegment-get-relativevirtualaddress.md)|检索部分开头的相对虚拟地址（RVA）。|
|[IDiaSegment::get_virtualAddress](../../debugger/debug-interface-access/idiasegment-get-virtualaddress.md)|检索部分开头的虚拟地址（VA）。|

## <a name="remarks"></a>备注
由于 DIA SDK 已经从相对虚拟地址的节偏移量执行翻译，因此大多数应用程序不会使用段映射中的信息。

## <a name="notes-for-callers"></a>调用方说明
通过调用[IDiaEnumSegments：： Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)或[IDiaEnumSegments：： Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)方法获取此接口。 有关详细信息，请参阅示例。

## <a name="example"></a>示例
此函数显示表中所有段的地址和最接近的符号。

```C++
void ShowSegments(IDiaTable *pTable, IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pSegments;
    if ( SUCCEEDED( pTable->QueryInterface(
                                _uuidof( IDiaEnumSegments ),
                               (void**)&pSegments )
                  )
       )
    {
        CComPtr<IDiaSegment> pSegment;
        while ( SUCCEEDED( hr = pSegments->Next( 1, &pSegment, &celt ) ) &&
                celt == 1 )
        {
            DWORD rva;
            DWORD seg;

            pSegment->get_addressSection( &seg );
            if ( pSegment->get_relativeVirtualAddress( &rva ) == S_OK )
            {
                printf( "Segment %i addr: 0x%.8X\n", seg, rva );
                pSegment = NULL;

                CComPtr<IDiaSymbol> pSym;
                if ( psession->findSymbolByRVA( rva, SymTagNull, &pSym ) == S_OK )
                {
                    CDiaBSTR name;
                    DWORD    tag;

                    pSym->get_symTag( &tag );
                    pSym->get_name( &name );
                    printf( "\tClosest symbol: %ws (%ws)\n",
                            name != NULL ? name : L"",
                            szTags[ tag ] );
                }
            }
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
- [IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)
- [IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)
