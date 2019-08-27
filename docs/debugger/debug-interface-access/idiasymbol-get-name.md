---
title: 'Idiasymbol:: Get_name |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_name method
ms.assetid: 050ec02f-b7b3-48fc-8e35-58bdf7d938b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ed872bd0cf90bef4433e3430ea8a7557213cbb4c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64809011"
---
# <a name="idiasymbolgetname"></a>IDiaSymbol::get_name
检索的符号名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_name ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回符号的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="example"></a>示例

```C++
IDiaSymbol* pType;
BSTR        name;
pType->get_name( &name );
```

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)