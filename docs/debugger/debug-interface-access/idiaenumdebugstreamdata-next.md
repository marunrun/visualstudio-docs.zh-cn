---
title: IDiaEnumDebugStreamData：： Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Next method
ms.assetid: 114171dd-38fd-4bd7-a702-8ff887ffc99b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: acdab0a565613194c67aa85484316a235c91dbf6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744795"
---
# <a name="idiaenumdebugstreamdatanext"></a>IDiaEnumDebugStreamData::Next
检索枚举序列中指定数目的记录。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG  celt,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[],
   ULONG* pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的记录数。

 cbData

中数据缓冲区的大小（以字节为单位）。

 pcbData

弄返回返回的字节数。 如果 `data` 为 NULL，则 `pcbData` 包含可用于所有请求记录的数据的总字节数。

 data[]

弄要使用调试流记录数据填充的缓冲区。

 pceltFetched

[in，out]返回 `data` 中的记录数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多记录，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)