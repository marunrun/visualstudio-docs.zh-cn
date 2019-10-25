---
title: IDiaEnumDebugStreams::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Item method
ms.assetid: 6b388fe1-eabc-4720-9d59-dc09b0ceaeac
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7a07669e36d397550c28d1cc4a5de2ad300763e6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744743"
---
# <a name="idiaenumdebugstreamsitem"></a>IDiaEnumDebugStreams::Item
通过索引或名称检索调试流。

## <a name="syntax"></a>语法

```C++
HRESULT Item (
    VARIANT                   index,
    IDiaEnumDebugStreamData** stream
);
```

#### <a name="parameters"></a>参数
索引

中要检索的调试流的索引或名称。 如果使用整数变量，则该变量的范围必须介于0到 `count`-1 之间，其中 `count` 为[IDiaEnumDebugStreams：： get_Count](../../debugger/debug-interface-access/idiaenumdebugstreams-get-count.md)方法返回的。

流

弄返回表示指定调试流的[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)对象。

## <a name="return-value"></a>返回值
如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="example"></a>示例

```C++
IDiaEnumDebugStreamData *GetStreamData(IDiaEnumDebugStreams *pStreamList,
                                       LONG whichStream)
{
    IDiaEnumDebugStreamData *pStreamData = NULL;
    if (pStreamList != NULL)
    {
        LONG numStreams = 0;
        if (pStreamList->get_count(&numStreams) == S_OK &&
            whichStream >= 0 && whichStream < numStreams)
        {
            VARIANT vIndex;
            vIndex.vt   = VT_I4;
            vIndex.lVal = whichStream;
            if (pStreamList->Item(vIndex,&pStreamData) != S_OK)
            {
                std::cerr << "Error retrieving stream " << whichStream << std::endl;
            }
        }
    }
    return(pStreamData);
}
```

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)
