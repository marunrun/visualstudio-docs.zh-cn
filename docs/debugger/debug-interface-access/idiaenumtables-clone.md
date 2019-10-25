---
title: IDiaEnumTables::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Clone method
ms.assetid: beb21109-b12c-44d8-8c1f-a332216b3713
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 522ac4080331c869c32585dfed789378b1271542
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743796"
---
# <a name="idiaenumtablesclone"></a>IDiaEnumTables::Clone
创建与当前枚举数包含相同枚举状态的枚举数。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumTables** ppenum
);
```

#### <a name="parameters"></a>参数
 `ppenum`

弄返回一个[IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)对象，该对象包含枚举器的副本。 这些表不会重复，只是枚举器。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)