---
title: IDiaFrameData::get_functionParent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_functionParent method
ms.assetid: f00b9ab1-d4da-4818-973a-58f8f0e66769
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 20f9dac750f9ff9723e4f3669f9e9a124d728a9a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830339"
---
# <a name="idiaframedatagetfunctionparent"></a>IDiaFrameData::get_functionParent
检索将封闭函数的帧数据接口。

## <a name="syntax"></a>语法

```C++
HRESULT get_functionParent ( 
   IDiaFrameData** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)封闭函数的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)