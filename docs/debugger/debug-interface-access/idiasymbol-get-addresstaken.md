---
title: IDiaSymbol::get_addressTaken | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressTaken method
ms.assetid: 0d366188-f5e1-4226-b392-58c09539d097
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f452aa01f29d25ad1674c6bc2f5494a745733793
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741061"
---
# <a name="idiasymbolget_addresstaken"></a>IDiaSymbol::get_addressTaken
检索一个标志，该标志指示另一个符号是否引用此符号的地址。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressTaken ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果其他符号引用此地址，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="example"></a>示例
 在下面的示例中，`B` 引用 `A`。 因此，符号 `A` 的 `get_addressTaken` 方法返回 `TRUE`。

```C++
int A  = 0;
int* B = &A;
```

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)