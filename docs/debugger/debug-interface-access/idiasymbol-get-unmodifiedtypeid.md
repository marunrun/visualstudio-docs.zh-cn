---
title: IDiaSymbol::get_unmodifiedTypeId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 4f7fc73c-f524-4d7a-b378-a9ab99a96104
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99d549a0edc56d48d686424c35f22fc7ea74438b
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62841180"
---
# <a name="idiasymbolgetunmodifiedtypeid"></a>IDiaSymbol::get_unmodifiedTypeId
检索原始 （未修改） 类型的 ID。

## <a name="syntax"></a>语法

```C++
HRESULT get_unmodifiedTypeId(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]一个指向`DWORD`保存此 id。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)