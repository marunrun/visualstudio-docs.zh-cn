---
title: IDiaStackWalkHelper::pdataForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::pdataByVA method
ms.assetid: fafc38fe-74dc-4726-9a51-eebf3a673d7f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d51736a80021847881db164c9e176a010124638
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741401"
---
# <a name="idiastackwalkhelperpdataforva"></a>IDiaStackWalkHelper::pdataForVA
返回与虚拟地址相关联的 PDATA 数据块。

## <a name="syntax"></a>语法

```C++
HRESULT pdataForVA( 
   ULONGLONG  va,
   DWORD      cbData,
   DWORD*     pcbData,
   BYTE*      pbData
);
```

#### <a name="parameters"></a>参数
 `va`

中指定要获取的数据的虚拟地址。

 `cbData`

中要获取的数据的大小（以字节为单位）。

 `pcbData`

弄返回获取的数据的实际大小（以字节为单位）。

 `pbData`

[in，out]使用请求的数据填充的缓冲区。 不能为 `NULL`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果指定地址没有 PDATA，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 编译单位的 PDATA （名为 "PDATA" 的部分）包含有关函数的异常处理的信息。

 调用方知道要返回多少数据，以便调用方无需询问可用数据量。 因此，如果 `pbData` 参数 `NULL`，此方法的实现就可以返回错误。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)