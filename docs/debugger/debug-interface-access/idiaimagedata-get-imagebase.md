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
ms.openlocfilehash: de8c333391530cd86c6fc66a8e6c36ce8cfecd5f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829057"
---
# <a name="idiaimagedatagetimagebase"></a>IDiaImageData::get_imageBase
检索其中应基于映像的内存位置。

## <a name="syntax"></a>语法

```C++
HRESULT get_imageBase ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回建议的图像的基值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 由于映像基冲突而进行映像可能会重新设定基址自动到未使用的内存位置在加载时。 此方法返回已在编译时存储在模块中的基本提示 （建议的内存位置）。

## <a name="see-also"></a>请参阅
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)