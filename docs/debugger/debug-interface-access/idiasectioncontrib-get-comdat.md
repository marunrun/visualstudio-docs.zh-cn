---
title: IDiaSectionContrib::get_comdat | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_comdat method
ms.assetid: 8bd9be8d-59ee-4698-b055-daba354b8dcc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 49502c0d693c7a309da9756f73c34df361b7d7bb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832521"
---
# <a name="idiasectioncontribgetcomdat"></a>IDiaSectionContrib::get_comdat
检索一个标志，指示了 COMDAT 记录的部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_comdat ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`的部分是 COMDAT 记录; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 COMDAT 记录是使封装的函数的链接器可见的通用对象文件格式 (COFF) 记录。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)