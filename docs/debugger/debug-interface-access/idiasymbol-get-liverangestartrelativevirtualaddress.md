---
title: IDiaSymbol::get_liveRangeStartRelativeVirtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartRelativeVirtualAddress
ms.assetid: 1da52539-9872-4c20-8eaa-74b6cb5f3b02
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ea82e9d1dee4b82e78ea3f6409acfdcfc30b2a27
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739896"
---
# <a name="idiasymbolget_liverangestartrelativevirtualaddress"></a>IDiaSymbol::get_liveRangeStartRelativeVirtualAddress
返回本地符号有效的地址范围的开头。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeStartRelativeVirtualAddress ( 
   DWORD* address
);
```

#### <a name="parameters"></a>参数
 `address`

弄返回地址范围的开头。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。 返回的相对虚拟地址是符号有效的范围的开始位置。

> [!NOTE]
> 返回的错误代码表示该符号没有活动范围信息。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)