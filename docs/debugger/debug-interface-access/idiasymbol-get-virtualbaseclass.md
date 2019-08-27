---
title: 'Idiasymbol:: Get_virtualbaseclass |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseClass method
ms.assetid: 474eddc6-bf16-4731-9145-6db2f2a0b4fd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c97290f878a8b3b0835c7e3ac33aa2ebecfb019
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64799267"
---
# <a name="idiasymbolgetvirtualbaseclass"></a>IDiaSymbol::get_virtualBaseClass
检索指定用户定义数据类型是否为虚拟基类的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualBaseClass ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`用户定义数据类型是否为虚拟基类; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)