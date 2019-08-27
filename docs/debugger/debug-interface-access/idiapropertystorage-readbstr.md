---
title: IDiaPropertyStorage::ReadBSTR |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBSTR
ms.assetid: 7214643b-3286-48ed-90aa-0fe95b4cae5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f0bff81499fe8ea66ce5d4f50616adfec44d3002
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839623"
---
# <a name="idiapropertystoragereadbstr"></a>IDiaPropertyStorage::ReadBSTR
读取`BSTR`属性组中的值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadBSTR ( 
   PROPID id,
   BSTR*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in]要读取的属性的标识符 (`PROPID`定义为 WTypes.h 中`ULONG`)。

 `pValue`

[out]返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。 返回`E_INVALIDARG`如果该属性的类型不是`BSTR`。

## <a name="remarks"></a>备注
 一个`BSTR`由 Windows 为零终止宽字符字符串定义。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)