---
title: IDiaSession::findSymbolsForAcceleratorPointerTag |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 95fd5e7a-c637-437e-b369-c864eef733c2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 72510e9e82c1ec6983075880d4335dee8c0ad23c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839233"
---
# <a name="idiasessionfindsymbolsforacceleratorpointertag"></a>IDiaSession::findSymbolsForAcceleratorPointerTag
在父 Accelerator 存根 （stub） 函数中返回指定的标记值对应于该变量的符号的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolsForAcceleratorPointerTag ( 
   IDiaSymbol*           parent,
   DWORD                 tagValue,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in]对应于要搜索的加速器存根 （stub） 函数 IDiaSymbol。

 `tagValue`

[in]指针标记值。

 `ppResult`

[out]一个指向`IDiaEnumSymbols`使用结果初始化的接口指针。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)