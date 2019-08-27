---
title: IDiaSymbol::findSymbolsForAcceleratorPointerTag |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: fb66852c-c5f7-4140-b9fe-20cb4e51a9fe
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7bf55f372b9beb0a4cb0feda0dc5869ee9eb7c5f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62827740"
---
# <a name="idiasymbolfindsymbolsforacceleratorpointertag"></a>IDiaSymbol::findSymbolsForAcceleratorPointerTag
返回 accelerator 指针中的标记数C++AMP 存根 （stub） 函数。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsForAccleratorPointerTag (
   DWORD             tagValue,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>参数
 `tagValue`

[in]为其找到 pointee 符号记录指针标记值。

 `ppResult`

[out]一个指向`IDiaEnumSymbols`使用结果初始化接口指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)