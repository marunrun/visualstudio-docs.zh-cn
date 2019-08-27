---
title: IDiaEnumFrameData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData interface
ms.assetid: 2ca7fd5a-b2fa-4b3a-9492-0263eafc435b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db06efe400106260556d8eab5fd644bbfc27f0c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833614"
---
# <a name="idiaenumframedata"></a>IDiaEnumFrameData
枚举数据源中包含的各种框架的数据元素。

## <a name="syntax"></a>语法

```
IDiaEnumFrameData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法`IDiaEnumFrameData`。

|方法|描述|
|------------|-----------------|
|[IDiaEnumFrameData::get__NewEnum](../../debugger/debug-interface-access/idiaenumframedata-get-newenum.md)|检索`IEnumVARIANT Interface`此枚举器的版本。|
|[IDiaEnumFrameData::get_Count](../../debugger/debug-interface-access/idiaenumframedata-get-count.md)|检索帧数据元素数。|
|[IDiaEnumFrameData::Item](../../debugger/debug-interface-access/idiaenumframedata-item.md)|通过索引中检索帧数据元素。|
|[IDiaEnumFrameData::Next](../../debugger/debug-interface-access/idiaenumframedata-next.md)|检索指定的数目的帧枚举序列中的数据元素。|
|[IDiaEnumFrameData::Skip](../../debugger/debug-interface-access/idiaenumframedata-skip.md)|跳过枚举序列中的帧数据元素的指定的数目。|
|[IDiaEnumFrameData::Reset](../../debugger/debug-interface-access/idiaenumframedata-reset.md)|将枚举序列重置到开头。|
|[IDiaEnumFrameData::Clone](../../debugger/debug-interface-access/idiaenumframedata-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|
|[IDiaEnumFrameData::frameByRVA](../../debugger/debug-interface-access/idiaenumframedata-framebyrva.md)|按相对虚拟地址 (RVA) 返回一个帧。|
|[IDiaEnumFrameData::frameByVA](../../debugger/debug-interface-access/idiaenumframedata-framebyva.md)|按虚拟地址 (VA) 返回一个帧。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方的说明
获取此接口从[idiasession:: Getenumtables](../../debugger/debug-interface-access/idiasession-getenumtables.md)方法。 请参阅详细信息的示例。

## <a name="example"></a>示例
此示例演示如何获取 (`GetEnumFrameData`函数)，并使用 (`ShowFrameData`函数)`IDiaEnumFrameData`接口。 请参阅[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)接口的示例`PrintFrameData`函数。

```C++

      IDiaEnumFrameData* GetEnumFrameData(IDiaSession *pSession)
{
    IDiaEnumFrameData* pUnknown    = NULL;
    REFIID             iid         = __uuidof(IDiaEnumFrameData);
    IDiaEnumTables*    pEnumTables = NULL;
    IDiaTable*         pTable      = NULL;
    ULONG              celt        = 0;

    if (pSession->getEnumTables(&pEnumTables) != S_OK)
    {
        wprintf(L"ERROR - GetTable() getEnumTables\n");
        return NULL;
    }
    while (pEnumTables->Next(1, &pTable, &celt) == S_OK && celt == 1)
    {
        // There is only one table that matches the given iid
        HRESULT hr = pTable->QueryInterface(iid, (void**)&pUnknown);
        pTable->Release();
        if (hr == S_OK)
        {
            break;
        }
    }
    pEnumTables->Release();
    return pUnknown;
}

void ShowFrameData(IDiaSession *pSession)
{
    IDiaEnumFrameData* pEnumFrameData = GetEnumFrameData(pSession);;

    if (pEnumFrameData != NULL)
    {
        IDiaFrameData* pFrameData;
        ULONG celt = 0;

        while(pEnumFrameData->Next(1, &pFrameData, &celt) == S_OK &&
              celt == 1)
        {
            PrintFrameData(pFrameData);
            pFrameData->Release();
        }
        pEnumFrameData->Release();
    }
}
```

## <a name="requirements"></a>要求
**标头：** dia2.h

**库：** diaguids.lib

**DLL:** msdia80.dll

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
