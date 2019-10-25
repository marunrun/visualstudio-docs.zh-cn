---
title: IDiaSymbol::get_liveRangeStartAddressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressSection
ms.assetid: 892b80ff-5957-4233-b4d7-6144167be289
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a23f0661d8af6417d754fd7a71c66c5dd3ef1135
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739910"
---
# <a name="idiasymbolget_liverangestartaddresssection"></a>IDiaSymbol::get_liveRangeStartAddressSection
返回本地符号有效的范围起始地址的部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeStartAddressSection ( 
   DWORD* section
);
```

#### <a name="parameters"></a>参数
 `section`

弄返回起始地址范围的部分。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

> [!NOTE]
> 返回的错误代码表示该符号没有活动范围信息。

## <a name="remarks"></a>备注
 由节和偏移量组成的地址是符号有效的范围的开始位置。

 若要获取地址的偏移量部分，请使用[IDiaSymbol：： get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md)。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)