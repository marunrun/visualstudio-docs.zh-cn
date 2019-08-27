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
ms.openlocfilehash: 6688844b5e5353d0d80ef2fb5fa2466a53f5f34a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840065"
---
# <a name="idiaframedatagetlengthlocals"></a>IDiaFrameData::get_lengthLocals
检索局部变量推送到堆栈上的字节的数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthLocals ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回局部变量的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 中的计划字符串解释通常使用此方法返回的值 (请参阅[idiaframedata:: Get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)程序字符串的定义的方法)。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)