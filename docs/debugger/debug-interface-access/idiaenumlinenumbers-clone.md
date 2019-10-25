---
title: IDiaEnumLineNumbers：： Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Clone method
ms.assetid: fcd2479a-8ff7-4aba-a737-06123c280d54
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 42e17066df5ece7efda46f2a389b5ae5756949ea
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744444"
---
# <a name="idiaenumlinenumbersclone"></a>IDiaEnumLineNumbers::Clone
创建与当前枚举数包含相同枚举状态的枚举数。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumLineNumbers** ppenum
);
```

#### <a name="parameters"></a>参数
 `ppenum`

弄返回一个[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)对象，该对象包含枚举器的副本。 行号不重复，只是枚举器.。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)