---
title: IDiaSymbol::get_isHLSLData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 4662058b-c505-4ccf-ae03-739a62c814ca
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 03b0bf45d4b8100f4ebfd1d6a61dc73547312fe6
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62836698"
---
# <a name="idiasymbolgetishlsldata"></a>IDiaSymbol::get_isHLSLData
指定此符号是否表示高级着色器语言 (HLSL) 数据。

## <a name="syntax"></a>语法

```C++
HRESULT get_isHLSLData(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`BOOL`，它指定此符号是否表示 HLSL 数据。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)