---
title: IDiaEnumSegments::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Clone method
ms.assetid: 93deaac6-72ab-4408-ba14-66174a618757
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9992b17155601284387981a9b424a77d3d9b5580
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829662"
---
# <a name="idiaenumsegmentsclone"></a>IDiaEnumSegments::Clone
创建一个包含当前枚举数形式的相同枚举状态的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumSegments** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out]返回[IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)对象，其中包含重复的枚举器。 不重复的段，仅枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)