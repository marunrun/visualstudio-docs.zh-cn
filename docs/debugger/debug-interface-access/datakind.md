---
title: DataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 31be0615fd7d1da279ecf414260af21cb8239dc8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745292"
---
# <a name="datakind"></a>DataKind
指示数据值的特定范围。

## <a name="syntax"></a>语法

```C++
enum DataKind {
    DataIsUnknown,
    DataIsLocal,
    DataIsStaticLocal,
    DataIsParam,
    DataIsObjectPtr,
    DataIsFileStatic,
    DataIsGlobal,
    DataIsMember,
    DataIsStaticMember,
    DataIsConstant
};
```

## <a name="elements"></a>元素
无法确定 DataIsUnknown 数据符号。

DataIsLocal 数据项是一个本地变量。

DataIsStaticLocal 数据项是一个静态局部变量。

DataIsParam 数据项是一个形参。

DataIsObjectPtr 数据项是一个对象指针（`this`）。

DataIsFileStatic 数据项是一个文件范围内的变量。

DataIsGlobal 数据项是一个全局变量。

DataIsMember 数据项是一个对象成员变量。

DataIsStaticMember 数据项是一个类静态变量。

DataIsConstant 数据项是一个常数值。

## <a name="remarks"></a>备注
此枚举中的值由[IDiaSymbol：： get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)方法返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)
