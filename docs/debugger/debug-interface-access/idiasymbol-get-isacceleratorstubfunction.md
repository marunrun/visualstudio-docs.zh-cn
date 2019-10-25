---
title: IDiaSymbol：： get_isAcceleratorStubFunction |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: cc4ea375-76f6-4ba8-baed-c5fa82108137
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: baf71d3be8916c18b16e4022a2af884617b5fd70
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72740304"
---
# <a name="idiasymbolget_isacceleratorstubfunction"></a>IDiaSymbol::get_isAcceleratorStubFunction
指示符号是否对应于为对应于 `parallel_for_each` 调用的快捷键编译的着色器的顶级函数符号。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAcceleratorStubFunction(
   BOOL* pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄一个指向 `BOOL` 的指针，该指针指示符号是否对应于为对应于 `parallel_for_each` 调用的快捷键编译的着色器的顶级函数符号。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)