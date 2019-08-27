---
title: IDiaFrameData::get_lengthProlog | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthProlog method
ms.assetid: 5f042ff1-e74e-430a-be34-d2cf1b18eff2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad162a8a29bd9432424ce64d00e820a0bfde1dd9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839948"
---
# <a name="idiaframedatagetlengthprolog"></a>IDiaFrameData::get_lengthProlog
检索块中的序言代码的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthProlog ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回的序言代码的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 序言代码是一系列的说明，可以保留寄存器、 设置的 CPU 的状态，并建立函数的堆栈。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)