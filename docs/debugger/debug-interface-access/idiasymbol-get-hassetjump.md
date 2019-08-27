---
title: IDiaSymbol::get_hasSetJump | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasSetJump method
ms.assetid: 22656206-dccf-40ed-b179-fc016d1b262a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d560cbff64a5134fa58ade4d562cb9fb073af48f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64785873"
---
# <a name="idiasymbolgethassetjump"></a>IDiaSymbol::get_hasSetJump
检索一个标志，指定该函数是否包含的一种用法[setjmp](/cpp/c-runtime-library/reference/setjmp)命令 (已与配对[longjmp](/cpp/c-runtime-library/reference/longjmp)命令时，它们构成异常处理的 C 样式方法)。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasSetJump(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`如果该函数包含`setjmp`命令; 否则，返回`FALSE`。

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
- [IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)
- [longjmp](/cpp/c-runtime-library/reference/longjmp)
- [setjmp](/cpp/c-runtime-library/reference/setjmp)