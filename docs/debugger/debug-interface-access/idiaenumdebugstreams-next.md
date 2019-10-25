---
title: IDiaEnumDebugStreams：： Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Next method
ms.assetid: eb8eae5a-be27-45f4-a7bd-6e4ef0652385
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 63b66729192c9c976ecd226ab21aad73b94bf9f2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744732"
---
# <a name="idiaenumdebugstreamsnext"></a>IDiaEnumDebugStreams::Next
检索枚举序列中指定数目的调试流。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG                     celt,
   IDiaEnumDebugStreamData** rgelt,
   ULONG*                    pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举器中的调试流的数目。

 rgelt

弄返回[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)对象的数组，这些对象表示要检索的调试流。

 pceltFetched

弄返回返回的调试流的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多的流，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)