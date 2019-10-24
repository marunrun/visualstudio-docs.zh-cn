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
ms.openlocfilehash: cd169ac890fa9f86d4eaa0e121da3f2c1387db2f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744231"
---
# <a name="idiaenumsegmentsclone"></a>IDiaEnumSegments::Clone
创建与当前枚举数包含相同枚举状态的枚举数。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumSegments** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

弄返回一个[IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)对象，该对象包含枚举器的副本。 分段不是重复的，只是枚举器。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)