---
title: IDiaEnumFrameData::frameByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByRVA method
ms.assetid: 4b8dec05-e76c-4cc4-9644-2369d583849f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f0a6636b692a3017adb6d8b9242dca62f397bf40
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744675"
---
# <a name="idiaenumframedataframebyrva"></a>IDiaEnumFrameData::frameByRVA
返回按相对虚拟地址（RVA）的帧。

## <a name="syntax"></a>语法

```C++
HRESULT frameByRVA( 
   DWORD           relativeVirtualAddress,
   IDiaFrameData** frame
);
```

#### <a name="parameters"></a>参数
 relativeVirtualAddress

中感兴趣的帧的 RVA。

 框架

弄返回一个[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，该对象表示包含提供的地址的帧。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有与指定地址匹配的帧数据，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)