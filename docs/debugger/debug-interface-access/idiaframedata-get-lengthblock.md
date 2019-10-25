---
title: IDiaFrameData::get_lengthBlock | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthBlock method
ms.assetid: 2e54deb7-7744-428e-913c-1d47a2aa89b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: da5b175c7e51e5ee8aaab29788f71219091d26f0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743578"
---
# <a name="idiaframedataget_lengthblock"></a>IDiaFrameData::get_lengthBlock
检索框架所描述的代码块的长度（以字节为单位）。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthBlock ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回框架中代码的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值通常用于程序字符串的解释（有关程序字符串的定义，请参见[IDiaFrameData：： get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)方法）。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)