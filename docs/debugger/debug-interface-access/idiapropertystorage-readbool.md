---
title: IDiaPropertyStorage::ReadBOOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBOOL
ms.assetid: ad1822db-4572-48f7-9919-f8137f6701f2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5cc189283d6e9910b0b01d3d3e1ca28165bf500
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839688"
---
# <a name="idiapropertystoragereadbool"></a>IDiaPropertyStorage::ReadBOOL
读取`BOOL`属性组中的值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadBOOL ( 
   PROPID id,
   BOOL*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in]要读取的属性的标识符 (`PROPID`定义为 WTypes.h 中`ULONG`)。

 `pValue`

[out]返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`E_INVALIDARG`如果该属性的类型不是`BOOL`。

## <a name="remarks"></a>备注
 一致的结果，将解释`BOOL`值，以便非零值都`TRUE`零值为`FALSE`。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)