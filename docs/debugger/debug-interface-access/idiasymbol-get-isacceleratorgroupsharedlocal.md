---
title: IDiaSymbol::get_isAcceleratorGroupSharedLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 17a20542-5b45-478f-bb80-0d56031aadb5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ac6a7582c6fa59665390cfdb6b613fff6e36709
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62836831"
---
# <a name="idiasymbolgetisacceleratorgroupsharedlocal"></a>IDiaSymbol::get_isAcceleratorGroupSharedLocal
检索一个标志，指示符号是否与组共享本地变量在编译的代码相对应C++AMP 快捷键。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorGroupSharedLocal(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]一个指向`BOOL`，该值指示符号是否与组共享本地变量在编译的代码相对应C++AMP 快捷键。 如果`TRUE`，则`get_baseDataSlot`和`get_baseDataOffset`方法可用于获取变量的存储位置信息。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)
- [IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)