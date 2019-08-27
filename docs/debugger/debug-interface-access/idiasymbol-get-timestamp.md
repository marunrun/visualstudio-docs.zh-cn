---
title: IDiaSymbol::get_timeStamp | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_timeStamp method
ms.assetid: 5d707b76-dbaa-4d88-86c3-6f3672cc6d4c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91f75ab56c8c34e2c58e0f0560422021299c9540
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64793694"
---
# <a name="idiasymbolgettimestamp"></a>IDiaSymbol::get_timeStamp
检索基础可执行文件的时间戳。

## <a name="syntax"></a>语法

```C++
HRESULT get_timeStamp ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回基础可执行文件的时间戳。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)