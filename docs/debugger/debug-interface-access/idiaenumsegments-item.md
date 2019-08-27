---
title: IDiaEnumSegments::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Item method
ms.assetid: ee44dd55-39a0-4b7b-97ff-2e1226eeb2bd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 87751dcca1e2109db53c9d6dd4594bc969ffc684
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833267"
---
# <a name="idiaenumsegmentsitem"></a>IDiaEnumSegments::Item
通过索引中检索一个段。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD         index,
   IDiaSegment** segment
);
```

#### <a name="parameters"></a>参数
 索引

[in]索引[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)要检索对象。 索引是 0 到范围内`count`-1，其中`count`返回的[idiaenumsegments:: Get_count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md)方法。

 段

[out]返回[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)对象，表示所需的段。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)