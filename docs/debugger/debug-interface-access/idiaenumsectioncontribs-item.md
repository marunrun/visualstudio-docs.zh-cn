---
title: IDiaEnumSectionContribs::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Item method
ms.assetid: 63a28f23-0ca0-44a7-b11b-ca0206d642a0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2cd51bd663087aa04a7ec4e60e5c4291a35d9193
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833280"
---
# <a name="idiaenumsectioncontribsitem"></a>IDiaEnumSectionContribs::Item
通过索引来检索部分发布内容。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD                index,
   IDiaSectionContrib** section
);
```

#### <a name="parameters"></a>参数
 索引

[in]索引[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)要检索对象。 索引是 0 到范围内`count`-1，其中`count`返回的[idiaenumsectioncontribs:: Get_count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)方法。

 section

[out]返回[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)对象，表示所需的部分中所占比例。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)