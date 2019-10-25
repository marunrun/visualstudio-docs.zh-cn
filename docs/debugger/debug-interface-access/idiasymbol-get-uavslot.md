---
title: IDiaSymbol：： get_uavSlot |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: a70648f2-3b25-439f-8099-239ac602515a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 077a0a7895e93714bfe7b64b658c59f4d38ead4e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739051"
---
# <a name="idiasymbolget_uavslot"></a>IDiaSymbol::get_uavSlot
检索 uav 槽。

## <a name="syntax"></a>语法

```C++
HRESULT get_uavSlot(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄指向保存 uav 槽的 `DWORD` 的指针。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)