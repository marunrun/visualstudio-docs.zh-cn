---
title: IDiaPropertyStorage::Enum |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::Enum
ms.assetid: 00e462da-980a-40b3-a2d6-75a25ee809e5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e39693f63ea706ecdfa30a9ce0202444f51d4f57
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839675"
---
# <a name="idiapropertystorageenum"></a>IDiaPropertyStorage::Enum
获取此集内的属性的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT Enum ( 
   IEnumSTATPROPSTG** ppenum
);
```

#### <a name="parameters"></a>参数
 `ppenum`

[out]返回`IEnumSTATPROPSTG`对象 （在 Microsoft.VisualStudio.OLE.Interop 命名空间） 表示的属性的枚举。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)