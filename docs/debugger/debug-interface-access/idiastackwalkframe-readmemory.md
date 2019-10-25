---
title: IDiaStackWalkFrame：： readMemory |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::readMemory method
ms.assetid: 7ab0b525-a5a7-4692-acad-e8c00fa9ab9a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae1201fca1fc25cce19b40b47d6435d02d80e1b4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741483"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
从映像读取内存。

## <a name="syntax"></a>语法

```C++
HRESULT readMemory ( 
   MemoryTypeEnum type,
   ULONGLONG va,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>参数
 `type`

中[MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)值之一，用于指定要访问的内存类型。

 `va`

中要开始读取的映像中的虚拟地址位置。

 `cbData`

中数据缓冲区的大小（以字节为单位）。

 `pcbData`

弄返回返回的字节数。 如果 `NULL` `data`，则 `pcbData` 包含可用数据的总字节数。

 `data`

弄要使用来自指定位置的数据进行填充的缓冲区。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)