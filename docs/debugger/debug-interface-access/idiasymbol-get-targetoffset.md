---
title: IDiaSymbol::get_targetOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_targetOffset method
ms.assetid: 7d141223-132a-409c-a5a4-94f97340313c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6a356eafb2afbd63613c0fe6be6b794822e5f91e
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64796536"
---
# <a name="idiasymbolgettargetoffset"></a>IDiaSymbol::get_targetOffset
检索转换 （thunk） 目标的偏移量的部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_targetOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回转换 （thunk） 目标地址的偏移量的部分。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)