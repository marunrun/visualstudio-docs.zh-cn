---
title: IDiaPropertyStorage::ReadLONG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadLONG
ms.assetid: 32054cbc-db55-4513-a1b4-de80e77aac8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2fb277368e23cf51a4d3d3b69226ee6bf093d6c3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839610"
---
# <a name="idiapropertystoragereadlong"></a>IDiaPropertyStorage::ReadLONG
读取`LONG`属性组中的值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadDLONG ( 
   PROPID id,
   LONG*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in]要读取的属性的标识符 (`PROPID`定义为 WTypes.h 中`ULONG`)。

 `pValue`

[out]返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`E_INVALIDARG`如果该属性的类型不是`LONG`。

## <a name="remarks"></a>备注
 一个`LONG`定义由 Windows 作为 32 位有符号整数。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)