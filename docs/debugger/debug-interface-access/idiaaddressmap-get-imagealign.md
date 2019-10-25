---
title: IDiaAddressMap::get_imageAlign | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_imageAlign method
ms.assetid: f1ba8071-669c-4cf7-9ac0-02f26d99f366
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa5394580a9b0db4600a7f1e67aa8bd7f7703542
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745091"
---
# <a name="idiaaddressmapget_imagealign"></a>IDiaAddressMap::get_imageAlign
检索当前图像的对齐方式。

## <a name="syntax"></a>语法

```C++
HRESULT get_imageAlign ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回可执行文件中的图像对齐值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 根据映像的加载和创建方式，图像与特定的内存边界对齐。 对齐通常在1、2、4、8、16、32或64字节边界上。 可以通过调用[IDiaAddressMap：:P ut_imagealign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)方法设置图像对齐。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::put_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)