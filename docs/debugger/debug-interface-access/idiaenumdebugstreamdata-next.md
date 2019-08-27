---
title: 'Idiaenumdebugstreamdata:: Next |Microsoft Docs'
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
ms.openlocfilehash: cf641fde4c03053496c732aa7904ddcad671af20
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838602"
---
# <a name="idiaenumdebugstreamdatanext"></a>IDiaEnumDebugStreamData::Next
检索指定的数目的枚举序列中的记录。

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

[in]要检索的记录数。

 cbData

[in]数据缓冲区，以字节为单位的大小。

 pcbData

[out]返回返回的字节数。 如果`data`为 NULL，则`pcbData`的所有请求的记录包含可用数据的字节总数。

 data[]

[out]是要调试流记录数据填充缓冲区。

 pceltFetched

[in、 out]返回中的记录数`data`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果没有更多记录。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)