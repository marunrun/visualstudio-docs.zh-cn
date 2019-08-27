---
title: IDiaEnumDebugStreams | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams interface
ms.assetid: 611caf4f-7a5f-4aa4-b909-52feeb3cc752
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b17e79e1bfefd5b6b23695f2f49d694c7148ae0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838140"
---
# <a name="idiaenumdebugstreams"></a>IDiaEnumDebugStreams
枚举数据源中包含的各种调试流。

## <a name="syntax"></a>语法

```
IDiaEnumDebugStreams : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaEnumDebugStreams`。

|方法|描述|
|------------|-----------------|
|[IDiaEnumDebugStreams::get__NewEnum](../../debugger/debug-interface-access/idiaenumdebugstreams-get-newenum.md)|检索`IEnumVARIANT`此枚举器的版本。|
|[IDiaEnumDebugStreams::get_Count](../../debugger/debug-interface-access/idiaenumdebugstreams-get-count.md)|检索调试流的数量。|
|[IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md)|通过索引检索调试流。|
|[IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)|检索指定的数目的枚举序列中的调试流。|
|[IDiaEnumDebugStreams::Skip](../../debugger/debug-interface-access/idiaenumdebugstreams-skip.md)|将跳过指定的数目的枚举序列中的调试流。|
|[IDiaEnumDebugStreams::Reset](../../debugger/debug-interface-access/idiaenumdebugstreams-reset.md)|将枚举序列重置到开头。|
|[IDiaEnumDebugStreams::Clone](../../debugger/debug-interface-access/idiaenumdebugstreams-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|

## <a name="remarks"></a>备注
调试流的内容是依赖于实现的未记录的数据格式。

## <a name="notes-for-callers"></a>调用方的说明
调用[idiasession:: Getenumdebugstreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)方法来获取`IDiaEnumDebugStreams`对象。

## <a name="example"></a>示例
此示例演示如何访问此接口中可用的数据流。 请参阅[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)接口的实现`PrintStreamData`函数。

```C++
void DumpAllDebugStreams( IDiaSession* pSession)
{
    IDiaEnumDebugStreams* pEnumStreams;

    wprintf(L"\n\n*** DEBUG STREAMS\n\n");
    // Retrieve an enumerated sequence of debug data streams
    if(pSession->getEnumDebugStreams(&pEnumStreams) == S_OK)
    {
        IDiaEnumDebugStreamData* pStream;
        ULONG celt = 0;

        for(; pEnumStreams->Next(1, &pStream, &celt) == S_OK; pStream = NULL)
        {
            PrintStreamData(pStream);
            pStream->Release();
        }
        pEnumStreams->Release();
    }
    else
    {
        wprintf(L"Failed to get any debug streams!\n");
    }
    wprintf(L"\n");
}
```

## <a name="requirements"></a>要求
标头：dia2.h

库： diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)
