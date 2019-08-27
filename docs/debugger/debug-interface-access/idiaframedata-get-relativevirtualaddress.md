---
title: IDiaFrameData::get_relativeVirtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_relativeVirtualAddress method
ms.assetid: de070ef4-6c9d-43ca-911c-5245cbcb8dbe
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 833ef811f6859d7b991ba5931803fc0a3d21745c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828995"
---
# <a name="idiaframedatagetrelativevirtualaddress"></a>IDiaFrameData::get_relativeVirtualAddress
检索该帧的代码相对虚拟地址 (RVA)。

## <a name="syntax"></a>语法

```C++
HRESULT get_relativeVirtualAddress ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回框架代码的相对虚拟地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)