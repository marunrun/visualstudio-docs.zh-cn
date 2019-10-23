---
title: IDiaSymbol：： get_intro |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intro method
ms.assetid: 101afe4a-4c57-45de-87b4-330394c6de10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4680af2d41ef3fa06a89784003c98982a09c2b63
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740348"
---
# <a name="idiasymbolget_intro"></a>IDiaSymbol::get_intro
检索一个标志，该标志指定该函数是否为引入虚函数。

## <a name="syntax"></a>语法

```C++
HRESULT get_intro ( 
    BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
`pRetVal`

弄如果函数是 "简介"，则返回 `TRUE`;否则，将返回 `FALSE`。

## <a name="return-value"></a>返回值
如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="example"></a>示例

```C++
class A {
    virtual int f1();
}
class B : public A {
    int f1();
}
```

@No__t_0 和 `B::f1` 均为虚函数，但 `A::f1` 是简介 virtual。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
