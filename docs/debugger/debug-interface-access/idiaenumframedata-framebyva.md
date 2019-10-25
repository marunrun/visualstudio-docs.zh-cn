---
title: IDiaEnumFrameData::frameByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByVA method
ms.assetid: 0b1e441b-710a-46d8-8060-bed39071c834
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9889a4f4add318209728bb09ac5c469c1fa836fe
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744648"
---
# <a name="idiaenumframedataframebyva"></a>IDiaEnumFrameData::frameByVA
返回按虚拟地址（VA）的帧。

## <a name="syntax"></a>语法

```C++
HRESULT frameByVA( 
   ULONGLONG       virtualAddress,
   IDiaFrameData** frame
);
```

#### <a name="parameters"></a>参数
 virtualAddress

中相关帧的 VA。

 框架

弄返回一个[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，该对象表示包含提供的地址的帧。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有与指定地址匹配的帧数据，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)