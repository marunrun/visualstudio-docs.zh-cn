---
title: IDiaAddressMap::put_imageAlign | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_imageAlign method
ms.assetid: f9ce875d-c263-43e5-a534-f34c37f9866f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b1a6bf037dc87d84fab21622571158fb0682f60
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745052"
---
# <a name="idiaaddressmapput_imagealign"></a>IDiaAddressMap::put_imageAlign
设置图像的对齐方式。

## <a name="syntax"></a>语法

```C++
HRESULT put_imageAlign ( 
   DWORD NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

中可执行文件的新图像对齐值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 映像（已加载可执行文件）与指定的内存边界对齐。 此对齐方式可能受到当前系统体系结构以及编译和链接时间选项的影响。 图像对齐始终在字节边界上。 以下图像对齐值有效：1、2、4、8、16、32和64字节边界。

 可以通过调用[IDiaAddressMap：： get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)方法检索当前图像对齐方式。

> [!NOTE]
> 此方法可被调用时已加载。 @No__t_0 方法通常在图像已移动或更改并且需要新对齐时使用。

## <a name="see-also"></a>请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)