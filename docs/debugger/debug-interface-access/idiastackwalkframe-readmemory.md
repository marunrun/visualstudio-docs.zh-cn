---
title: 'Idiastackwalkframe:: Readmemory |Microsoft Docs'
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
ms.openlocfilehash: 82ef0d25e796f9e04ecdcfd0c54a7312b9c9edad
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62837909"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
从图像中读取内存。

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

[in]之一[MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)枚举值，指定要访问的内存的类型。

 `va`

[in]要开始读取图像中的虚拟地址位置。

 `cbData`

[in]数据缓冲区，以字节为单位的大小。

 `pcbData`

[out]返回返回的字节数。 如果`data`是`NULL`，然后`pcbData`包含可用数据的字节总数。

 `data`

[out]若要使用从指定的位置的数据填充缓冲区。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)