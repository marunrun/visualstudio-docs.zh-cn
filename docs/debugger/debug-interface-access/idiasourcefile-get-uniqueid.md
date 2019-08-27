---
title: IDiaSourceFile::get_uniqueId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_uniqueId method
ms.assetid: e0b8dbc0-6061-4f31-bead-2cd72be44e41
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c4a204e04c1c99dcbe8c6ba6d5e3457ca875dde4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832248"
---
# <a name="idiasourcefilegetuniqueid"></a>IDiaSourceFile::get_uniqueId
检索一个简单的整数密钥值，该值是唯一的此映像。

## <a name="syntax"></a>语法

```C++
HRESULT get_uniqueId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回一个简单的整数密钥值，该值是唯一的此映像。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 而不是字符串可加快行编号处理键进行比较。

## <a name="see-also"></a>请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)