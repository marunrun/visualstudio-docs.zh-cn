---
title: 'Idiasymbol:: Get_nostackordering |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noStackOrdering method
ms.assetid: a1753917-705b-4165-9880-d05e91e6dcb4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d36a934fe9475613e916d51290ac6f8960a6b42
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64791997"
---
# <a name="idiasymbolgetnostackordering"></a>IDiaSymbol::get_noStackOrdering
此函数可检索一个标志，指示是否可以作为堆栈缓冲区检查的一部分实现没有堆栈排序 ([/GS （缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)编译器选项)。

## <a name="syntax"></a>语法

```C++
HRESULT get_noStackOrdering(
   BOOL *pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果没有堆栈的排序方式可以实现一部分堆栈缓冲区检查; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/GS（缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)