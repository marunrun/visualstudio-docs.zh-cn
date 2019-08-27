---
title: IDiaImageData::get_relativeVirtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_relativeVirtualAddress method
ms.assetid: e6d6deee-dc12-4b38-af15-f917b2d4368e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c6a0ff03784df581fc2f6c57b51b896096d97bba
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830209"
---
# <a name="idiaimagedatagetrelativevirtualaddress"></a>IDiaImageData::get_relativeVirtualAddress
检索虚拟内存中的位置相对于应用程序的模块。

## <a name="syntax"></a>语法

```C++
HRESULT get_relativeVirtualAddress ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回该模块的相对虚拟内存偏移量。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)