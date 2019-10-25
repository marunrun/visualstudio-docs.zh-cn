---
title: IDiaSymbol：： get_container |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_container method
ms.assetid: 24e832eb-80b3-484c-a41b-11477ec9de99
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0533eb2cdea1dd3e1bea3d64e2b94ce29a09353d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740778"
---
# <a name="idiasymbolget_container"></a>IDiaSymbol::get_container
此函数检索一个指针，该指针指向表示此符号的父/容器的符号。

## <a name="syntax"></a>语法

```C++
HRESULT get_container(
   IDiaSymbol **pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回一个指向 `IDiaSymbol` 的指针，该指针包含有关此符号的容器的信息。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，将返回 S_FALSE 或错误代码。

> [!NOTE]
> 返回值为 S_FALSE 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)