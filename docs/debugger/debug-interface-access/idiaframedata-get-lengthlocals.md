---
title: IDiaFrameData::get_lengthLocals | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthLocals method
ms.assetid: 51fe15c3-4cd6-4a06-8a41-a56502209762
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff67d3b7e9466451c7e7f79bf4137ec21f629e04
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743600"
---
# <a name="idiaframedataget_lengthlocals"></a>IDiaFrameData::get_lengthLocals
检索推送到堆栈上的局部变量的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthLocals ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回局部变量的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值通常用于程序字符串的解释（有关程序字符串的定义，请参见[IDiaFrameData：： get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)方法）。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)