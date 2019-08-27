---
title: IDiaSymbol::get_sizeInUdt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: a82ab896-0185-46a4-b4d5-babfcc660fe1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b0fa2172d1a56fb7b4730a51959c0b73bdfc9461
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62835900"
---
# <a name="idiasymbolgetsizeinudt"></a>IDiaSymbol::get_sizeInUdt
检索用户定义类型的成员的大小。

## <a name="syntax"></a>语法

```C++
HRESULT get_sizeInUdt(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`DWORD`，指定该成员的大小。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)