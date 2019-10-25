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
ms.openlocfilehash: 809de8589302ddc35a14e2ea0663248a163176e6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743625"
---
# <a name="idiaframedataget_functionparent"></a>IDiaFrameData::get_functionParent
检索封闭函数的帧数据接口。

## <a name="syntax"></a>语法

```C++
HRESULT get_functionParent ( 
   IDiaFrameData** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回封闭函数的[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)