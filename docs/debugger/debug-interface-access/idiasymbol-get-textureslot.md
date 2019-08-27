---
title: IDiaSymbol::get_textureSlot |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 166a1a3a-2e10-4baa-ace1-9104b56185ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b480cfee85af750addddbbc195881adab002e07c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62841537"
---
# <a name="idiasymbolgettextureslot"></a>IDiaSymbol::get_textureSlot
检索纹理槽。

## <a name="syntax"></a>语法

```C++
HRESULT get_textureSlot(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`DWORD`保存纹理槽。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)