---
title: IDiaImageData::get_imageBase | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_imageBase method
ms.assetid: 4ba3d9e4-b205-4ee6-a41d-6996972f1f85
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7887fea30b04f4ebb6605169c58551122eccf73d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743438"
---
# <a name="idiaimagedataget_imagebase"></a>IDiaImageData::get_imageBase
检索图像应基于的内存位置。

## <a name="syntax"></a>语法

```C++
HRESULT get_imageBase ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回建议的图像基数值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 由于映像基本冲突，加载时可能会自动将映像变基到未使用的内存位置。 此方法返回在编译时存储在模块中的基本提示（建议的内存位置）。

## <a name="see-also"></a>请参阅
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)