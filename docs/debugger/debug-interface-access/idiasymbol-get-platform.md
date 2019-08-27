---
title: 'Idiasymbol:: Get_platform |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_platform method
ms.assetid: dff1c1eb-bcb2-4275-bb07-f2fdc076d6fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6df21b974489004a27847e307089b1a65715b076
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64813431"
---
# <a name="idiasymbolgetplatform"></a>IDiaSymbol::get_platform
检索用于编译将编译单位的平台类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_platform ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个值从[CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md)枚举，用于指定平台的编译时将编译单位类型。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CV_CPU_TYPE_e 枚举](../../debugger/debug-interface-access/cv-cpu-type-e.md)