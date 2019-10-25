---
title: MemoryTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e0710ec5cdfcfcb59407d18b43b885603f017fdb
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738632"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
指定要访问的内存类型。

## <a name="syntax"></a>语法

```C++
enum MemoryTypeEnum {
    MemTypeCode,
    MemTypeData,
    MemTypeStack,
    MemTypeAny = -1
};
```

#### <a name="parameters"></a>参数
`MemTypeCode` 仅访问代码内存。

`MemTypeData` 访问数据或堆栈内存。

`MemTypeStack` 仅访问堆栈内存。

`MemTypeAny` 访问任意类型的内存。

## <a name="remarks"></a>备注
此枚举中的值将传递给[IDiaStackWalkHelper：： readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)方法，以限制对不同类型的内存的访问。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
