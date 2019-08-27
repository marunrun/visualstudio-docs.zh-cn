---
title: IDiaSymbol::get_numberOfModifiers |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 61ff7431-1994-4f7e-a182-1817f16f60a9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 74a83a83a805aa86d10b3c051ac1c6fc39f36f14
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62835979"
---
# <a name="idiasymbolgetnumberofmodifiers"></a>IDiaSymbol::get_numberOfModifiers
检索应用于原始类型的修饰符的数目。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfModifiers(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`DWORD`，它指定应用于原始类型的修饰符的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)