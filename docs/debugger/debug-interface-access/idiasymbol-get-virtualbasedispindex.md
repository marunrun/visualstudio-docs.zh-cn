---
title: 'Idiasymbol:: Get_virtualbasedispindex |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseDispIndex method
ms.assetid: 5561a3cb-2c82-41cf-9217-3ee2b1e1d1d1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 435957fed1d6805adb8e1c982368d9b16ca76885
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64796490"
---
# <a name="idiasymbolgetvirtualbasedispindex"></a>IDiaSymbol::get_virtualBaseDispIndex
检索虚拟基的偏移量表中的符号的索引。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualBaseDispIndex (
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回到虚拟基的偏移量表的索引。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)