---
title: IDiaSymbol：： get_hasLongJump |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasLongJump method
ms.assetid: 14484cb1-43b0-47a1-a9a8-081b55566886
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8fb1e23d252b7cb4f2685a9b07d6e3e92db801bd
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740506"
---
# <a name="idiasymbolget_haslongjump"></a>IDiaSymbol::get_hasLongJump
检索一个标志，该标志指定该函数是否包含[longjmp](/cpp/c-runtime-library/reference/longjmp)命令的使用（与[setjmp](/cpp/c-runtime-library/reference/setjmp)命令成对出现，它们构成了异常处理的 C 样式方法）。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasLongJump
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄如果函数包含 `longjmp` 命令，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)
- [longjmp](/cpp/c-runtime-library/reference/longjmp)
- [setjmp](/cpp/c-runtime-library/reference/setjmp)