---
title: UdtKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- UdtKind enumeration
ms.assetid: 400b59b9-373c-42cb-aae1-570494214328
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 511beae100529f0db555eca0a8ddb995d7a335d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853512"
---
# <a name="udtkind"></a>UdtKind
介绍不同的用户定义类型 (UDT)。

## <a name="syntax"></a>语法

```C++
enum UdtKind {
    UdtStruct,
    UdtClass,
    UdtUnion,
    UdtInterface
};
```

## <a name="elements"></a>元素
UdtStruct UDT 是一种结构。

UdtClass UDT 是一个类。

UdtUnion UDT 是一个联合。

UdtInterface UDT 是一个接口。

## <a name="remarks"></a>备注
返回此枚举中的值[idiasymbol:: Get_udtkind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)方法。

## <a name="requirements"></a>要求
标头： cvconst.h

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)
