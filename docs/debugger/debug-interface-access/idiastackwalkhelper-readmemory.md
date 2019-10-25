---
title: IDiaStackWalkHelper：： readMemory |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 57afd033b2d969a4ed57dc713b2c4266e0ead632
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741366"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
从可执行文件的图像的内存中读取数据块。

## <a name="syntax"></a>语法

```C++
HRESULT readMemory( 
   enum MemoryTypeEnum type,
   ULONGLONG           va,
   DWORD               cbData,
   DWORD*              pcbData,
   BYTE*               pbData
);
```

#### <a name="parameters"></a>参数
 `type`

中[MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)枚举中的一个值，该值指定要读取的内存类型。

 va

中要从其开始读取的映像中的虚拟地址。

 `cbData`

中数据缓冲区的大小（以字节为单位）。

 `pcbData`

弄返回实际读取的字节数。 如果 `NULL` `pbData`，则这是可用数据的总字节数。

 `pbData`

[in，out]填充内存读取的缓冲区。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)