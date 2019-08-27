---
title: IDiaSymbol::get_classParent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_classParent method
ms.assetid: 99db875a-caae-4d60-ae70-64bc8a9f6fba
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c6419153777b5af071b59b6b7888c4f18f228b1
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64830573"
---
# <a name="idiasymbolgetclassparent"></a>IDiaSymbol::get_classParent
检索类父级的符号的引用。

## <a name="syntax"></a>语法

```C++
HRESULT get_classParent ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)表示类父级的符号的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="remarks"></a>备注
 可以是类的父级的符号的类型均记录在[符号类型的类层次结构的](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)