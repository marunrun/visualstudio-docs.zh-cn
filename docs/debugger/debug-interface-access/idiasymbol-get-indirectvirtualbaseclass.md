---
title: IDiaSymbol：： get_indirectVirtualBaseClass |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_indirectVirtualBaseClass method
ms.assetid: 853b5c6f-e1cb-4675-ad36-9ee16e3341c3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 32aa963aecc2e44ea2eb808ab5932df8a72fb33f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740392"
---
# <a name="idiasymbolget_indirectvirtualbaseclass"></a>IDiaSymbol::get_indirectVirtualBaseClass
检索一个标志，该标志指定用户定义数据类型是否为间接虚拟基类。

## <a name="syntax"></a>语法

```C++
HRESULT get_indirectVirtualBaseClass ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄如果用户定义数据类型为间接虚拟基类，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)