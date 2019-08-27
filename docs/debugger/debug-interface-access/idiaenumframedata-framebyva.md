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
ms.openlocfilehash: 62999d8b8dc0313e9ca5086dc4737d7a41db1c87
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838215"
---
# <a name="idiaenumframedataframebyva"></a>IDiaEnumFrameData::frameByVA
按虚拟地址 (VA) 返回一个帧。

## <a name="syntax"></a>语法

```C++
HRESULT frameByVA( 
   ULONGLONG       virtualAddress,
   IDiaFrameData** frame
);
```

#### <a name="parameters"></a>参数
 virtualAddress

[in]弗吉尼亚州的感兴趣的帧。

 框架

[out]返回[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，表示包含提供的地址的帧。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果任何帧数据与指定的地址相不匹配。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)