---
title: IDiaFrameData::get_allocatesBasePointer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_allocatesBasePointer method
ms.assetid: 8a33db5d-008c-4fe5-b64f-210c9b77f686
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 283ef71b32c186956804cb3afe121af53a99abfc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743642"
---
# <a name="idiaframedataget_allocatesbasepointer"></a>IDiaFrameData::get_allocatesBasePointer
检索一个标志，该标志指示是否为此地址范围内的代码分配基指针。 已弃用此方法。

## <a name="syntax"></a>语法

```C++
HRESULT get_allocatesBasePointer ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果分配基指针，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此属性应仅由以前访问过 FPO_DATA 的代码使用，或在[IDiaFrameData：： get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)方法返回的程序字符串 `NULL` 时使用。 否则，程序字符串将包含计算以前寄存器值所需的所有信息。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)